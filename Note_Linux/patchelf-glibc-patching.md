# Patching an ELF Binary to Use a Custom glibc with `patchelf`

## Context

This guide covers how to redirect an ELF binary to use a custom-built glibc installation
instead of the system one. This is a non-trivial operation because `libc.so.6` and the
dynamic linker `ld-linux-x86-64.so.2` are tightly coupled and must always come from the
**same glibc build**.

---

## Prerequisites

- `patchelf` installed on the system
- A fully built and installed custom glibc, with **all files being real binaries** — no symlinks pointing back to system components
- The following files must be present in your custom lib directory (e.g. `/home/user/myglibc/lib/`):
  - `ld-linux-x86-64.so.2` — real binary, not a symlink
  - `libc.so.6`
  - `libm.so.6`
  - `libpthread.so.0`
  - `libdl.so.2`

> ⚠️ **Critical:** Verify each file with `ls -la` and `file` to confirm they are real ELF binaries.
> A symlink back to the system linker will cause a segfault at runtime.

---

## Step 1 — Audit the Binary Before Touching It

```bash
# Inspect current shared library dependencies
ldd ./your-binary

# Inspect current rpath
patchelf --print-rpath ./your-binary

# Inspect current interpreter
patchelf --print-interpreter ./your-binary
```

Save this output as your baseline. You will compare against it after every change.

---

## Step 2 — Back Up the Binary

```bash
cp ./your-binary ./your-binary.orig
```

`patchelf` modifies files in place. Always keep an unmodified copy.

---

## Step 3 — Set the Interpreter

Point the binary to the dynamic linker from your custom glibc build, not the system one.

```bash
patchelf --set-interpreter /home/user/myglibc/lib/ld-linux-x86-64.so.2 ./your-binary
```

> ⚠️ This is the step most often missed. Without it, the system `ld.so` drives execution
> and will be mismatched with your custom `libc.so.6`, causing a **segfault**.

---

## Step 4 — Set the RPATH

Set the rpath to include:
1. Your custom glibc lib directory **first** — so `libc.so.6`, `libm.so.6` etc. resolve from there
2. The system GCC runtime directory — so `libgcc_s.so.1` (which is **not** part of glibc) can still be found

```bash
patchelf --set-rpath '/home/user/myglibc/lib:/lib/x86_64-linux-gnu' ./your-binary
```

> ⚠️ Do not confuse `/lib` with `/lib/x86_64-linux-gnu`. On Debian/Ubuntu multiarch systems
> these are different directories. `libgcc_s.so.1` lives in the latter.

---

## Step 5 — Verify the Changes

```bash
# Check interpreter was updated
patchelf --print-interpreter ./your-binary

# Check rpath was updated
patchelf --print-rpath ./your-binary

# Full dependency resolution check
ldd ./your-binary
```

### Expected `ldd` output shape

| Library | Expected resolution path |
|---|---|
| `libc.so.6` | `/home/user/myglibc/lib/libc.so.6` |
| `libm.so.6` | `/home/user/myglibc/lib/libm.so.6` |
| `libgcc_s.so.1` | `/lib/x86_64-linux-gnu/libgcc_s.so.1` |
| interpreter | `/home/user/myglibc/lib/ld-linux-x86-64.so.2` |

> ⚠️ Any line showing `not found` is a hard blocker. The binary will fail at runtime.

---

## Step 6 — Deeper Verification with `readelf`

Do not rely solely on `ldd` — it can produce misleading output when the interpreter is a symlink.
Use `readelf` to inspect the ELF metadata directly.

```bash
# Confirm PT_INTERP segment
readelf -l ./your-binary | grep interpreter

# Confirm RUNPATH/RPATH tag in dynamic section
readelf -d ./your-binary | grep -E 'RPATH|RUNPATH'
```

---

## Step 7 — Test Execution

Run the binary directly. If all libraries resolve correctly it will execute normally.
If something is still wrong, you will get a precise error message rather than a vague segfault.

---

## Common Errors and Root Causes

| Error | Root cause |
|---|---|
| Segfault on startup | Interpreter (`ld.so`) and `libc.so.6` are from different glibc builds |
| `libgcc_s.so.1: cannot open shared object file` | Rpath set to `/lib` instead of `/lib/x86_64-linux-gnu` |
| `ldd` shows correct paths but binary still fails | Interpreter is a symlink back to the system linker |
| Binary works on build machine but not target | Custom lib directory contains symlinks to host system paths |

---

## Key Principles

- **`libc.so.6` and `ld-linux-x86-64.so.2` are a matched pair.** Never mix them across builds.
- **`libgcc_s.so.1` is a GCC runtime library, not part of glibc.** It does not need to come from your custom build.
- **`--replace-needed` is the wrong tool for `libc.so.6`.** The problem is always the loader/library pairing, not the library name.
- **`ldd` output can be misleading** when symlinks are involved. Always cross-check with `readelf`.
- **Explicit rpath disables implicit system search paths.** Once set, every required library must be reachable from the declared paths.
- **Always verify with `ls -la` and `file`** that your custom lib directory contains real ELF binaries, not symlinks.

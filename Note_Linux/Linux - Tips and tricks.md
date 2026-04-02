command `source` or `.` will execute the command or script inside the current environment.

`.so` -> shared object linked at runtime.

## RPATH
run-time search path

## Patch an elf binary
### Tool 
- patchelf
- ldd
- ldconfig
## Interactive and non-interactive shell
Interactive shell expect input.
non-interactive shell are the one executed with a script.

## Implicit relative path

```bash
challenge/run # Work if in the same directory as challenge
```

## Explicit relative path
```bash
./challenge/run
```

`~ expand to an absolute path`

## Manual
/usr/share/man

## FD
`>&` redirect a file descriptor to another like, 2>& 1 redirect the standard error into the standard input.

tee command duplicate the stdin into the stdout and file.
# Source
[[Source Linux]]
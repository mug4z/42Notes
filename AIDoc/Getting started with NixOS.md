# Learn NixOS by declaring, not installing

An experienced Linux user should start NixOS by unlearning one habit: you do not change the system, you describe it. NixOS is a Linux distribution built entirely from a single Nix expression. Every package lives in an immutable, hash-addressed path under `/nix/store`, and every `nixos-rebuild` produces a new bootable generation that you can roll back to. The fastest route is short and mostly official. Read "How Nix works", try NixOS in a VM, learn the Nix language basics and the module system on nix.dev, then edit the installer-generated `configuration.nix` with search.nixos.org open beside you. Put the config in git, and move to a flake (or npins) once you need pinning or inputs from outside nixpkgs. Most of the time newcomers waste goes into problems that are well documented: untracked files that flakes cannot see, downloaded binaries that will not run, bumping `system.stateVersion`, a full `/boot`, outdated tutorials and LLM answers, and copying someone else's huge config. The current stable release as of October 2026 is **NixOS 26.05 "Yarara"**, supported until 31 December 2026, with 26.11 "Zokor" next ([NixOS 26.05 announcement](https://nixos.org/blog/announcements/2026/nixos-2605/)). This report sets out the concepts, the differences from Debian, Ubuntu and Arch, a recommended starting path, an annotated link list, and a pitfall checklist.

## NixOS turns one expression into an entire bootable system

Four layers share the name. **Nix** is a purely functional deployment system from Eelco Dolstra's 2006 thesis. It stores components "under path names that contain cryptographic hashes of all inputs involved in building the component", which "prevents undeclared dependencies and enables support for side-by-side deployment". It also delivers atomic upgrades and **O(1) rollbacks** ([Dolstra thesis](https://edolstra.github.io/pubs/phd-thesis.pdf)). The **Nix language** is "a domain-specific, purely functional, lazily evaluated, dynamically typed programming language" whose job is to describe derivations, which are sandboxed build recipes ([nix.dev language tutorial](https://nix.dev/tutorials/nix-language)). **Nixpkgs** is the package collection and standard library (`lib`) written in that language. **NixOS** is the `nixos/` part of Nixpkgs. In it, `/etc/nixos/configuration.nix` is a function that takes `config`, `pkgs` and other arguments and returns option definitions ([NixOS manual](https://nixos.org/manual/nixos/stable/)).

The store model is what makes NixOS behave differently. A store path is `/nix/store/<32-char digest>-<name>` ([Nix manual: store path](https://nix.dev/manual/nix/latest/store/store-path)). A *closure* is everything reachable from a path by following references, and it is the unit of deployment. Binary caches ("substituters") serve prebuilt outputs, so most builds are downloads ([Nix manual: glossary](https://nix.dev/manual/nix/latest/glossary)). Nothing is deleted on uninstall. The garbage collector removes only what no profile generation still uses ([Nix manual: garbage collection](https://nix.dev/manual/nix/latest/package-management/garbage-collection)).

Your configuration is a set of **modules** that `lib.evalModules` merges into one `config`. Option types decide how definitions merge: list options from several modules are concatenated, while defining a `str` option twice is an error. Conflicts are settled by priority, and the lower number wins: `mkDefault` is **1000**, a plain definition is **100** and `mkForce` is **50** ([nixpkgs lib/modules.nix](https://raw.githubusercontent.com/NixOS/nixpkgs/master/lib/modules.nix); [nix.dev module deep dive](https://nix.dev/tutorials/module-system/deep-dive)). `nixos-rebuild switch` builds the result, makes it the boot default and activates it. `test` activates it without a boot entry, `boot` applies it at the next reboot only, and `build-vm` gives you a QEMU VM. Every rebuild adds a boot menu entry, so rollback costs nothing ([NixOS manual](https://nixos.org/manual/nixos/stable/)). Here is a short module that shows all the moving parts:

```nix
{ config, lib, pkgs, ... }: {
  imports = [ ./hardware-configuration.nix ];
  options.my.desktop.enable = lib.mkEnableOption "desktop";
  config = lib.mkMerge [
    { networking.hostName = lib.mkDefault "box"; }        # priority 1000: easy to override
    (lib.mkIf config.my.desktop.enable {                   # lazy condition, no recursion
      environment.systemPackages = [ pkgs.firefox ];
    })
  ];
}
```

Two parallel ways of supplying Nixpkgs exist. **Channels** are mutable, Hydra-tested snapshots found through `NIX_PATH` and `<nixpkgs>`. **Flakes** are git trees with a `flake.nix` (`inputs` plus an `outputs` function) and a `flake.lock` that pins every transitive input ([Nix manual: nix flake](https://nix.dev/manual/nix/latest/command-ref/new-cli/nix3-flake)). In upstream Nix 2.35, flakes and the new `nix` CLI are **still officially experimental** and must be enabled with `experimental-features = nix-command flakes` ([Nix manual: experimental features](https://nix.dev/manual/nix/latest/development/experimental-features)). Even so, **78.9% of 2025 survey respondents use flakes**, and a July 2026 Discourse debate ended without any stabilization timeline ([Discourse survey discussion](https://discourse.nixos.org/t/discussion-of-flakes-from-2025-nixos-community-survey-report/78853)). Two downstream implementations matter here. Determinate Nix 3.0 offers a formal flake stability guarantee ([Determinate Systems](https://determinate.systems/blog/determinate-nix-30)), and Lix, a volunteer CppNix fork, keeps flakes but has frozen their feature set ([Lix](https://lix.systems/about/)). **Home Manager** applies the same module system to `$HOME`: dotfiles, user packages and user services. It runs standalone or as a NixOS module activated by `nixos-rebuild`, and its branch must match your Nixpkgs release (`release-26.05` with 26.05, `master` with unstable) ([Home Manager manual](https://nix-community.github.io/home-manager/installation/nixos.html)).

## Debian, Ubuntu and Arch habits fail in five predictable places

The core difference is where state lives. apt and pacman install into one shared FHS tree, so only one version of each library can exist. That is why Arch does not support partial upgrades and insists on `pacman -Syu` ([Manjaro mirror of ArchWiki text](https://wiki.manjaro.org/index.php/Special:MobileDiff/3402)). Nix "never overwrite[s] packages in the Nix store", and "you can have multiple versions or variants of a package installed at the same time" ([Nix manual: introduction](https://nix.dev/manual/nix/stable/introduction)). To install something, you add a line to the configuration and rebuild.

| Aspect | NixOS 26.05 | Debian 13 | Ubuntu 26.04 LTS | Arch |
|---|---|---|---|---|
| Package tool | Nix (`nixos-rebuild`, `nix`) | apt/dpkg | apt/dpkg (+ snap) | pacman (+ AUR helpers) |
| Install location | `/nix/store/<hash>-name`, no FHS `/usr` | FHS `/usr` | FHS `/usr` | FHS `/usr` |
| Side-by-side versions | Yes | No | No | No; partial upgrades unsupported |
| Rollback | Built in: generations in boot menu | None native | None native | None native; btrfs snapshots optional |
| System config | Declarative; `/etc` generated | Hand-edited `/etc`, conffile prompts | Hand-edited `/etc` | Hand-edited `/etc`, `.pacnew` files |
| Releases | YY.05 and YY.11, plus unstable | Stable releases | LTS plus interim | Rolling |
| Support window | ~7 months (26.05 until 2026-12-31) | Full to 2028-08-09, LTS to 2030-06-30 | 5 years standard, 10 with Pro | Always latest |
| Repology projects | 119k unstable / 115k 26.05 | 38k (13), 42k (sid) | 40k | 12k official + 97k AUR |
| Share of packages at newest version | 83.5% unstable / 68.1% 26.05 | 40.7% (13) | 47.7% | 86.5% official |
| Generic prebuilt binaries | Need nix-ld, patchelf, steam-run or buildFHSEnv | Work | Work | Work |

Sources: [Nix manual](https://nix.dev/manual/nix/stable/introduction), [NixOS 26.05 announcement](https://nixos.org/blog/announcements/2026/nixos-2605/), [Debian trixie](https://www.debian.org/releases/trixie/), [Ubuntu 26.04 release notes](https://documentation.ubuntu.com/release-notes/26.04/), [Repology statistics](https://repology.org/repositories/statistics/total) (fetched 2026-10-25).

**Configuration management** changes the most. NixOS generates `/etc` from your config. Since 24.05 it can optionally mount `/etc` as an overlayfs, a feature still marked experimental ([nixpkgs commit](https://code.ornl.gov/nix/nixpkgs/-/commit/18e517662107874602de67a10d2265a021d2e693)). So there is no `.pacnew` merge, and a setting you delete is simply absent from the next generation. That is the real advantage over Ansible, which only converges the tasks it lists. **Upgrades** between releases are a change of channel or flake input, and you can roll them back from the boot menu. A rollback restores the OS closure, though, not `/home`, `/var` or database state ([NixOS manual](https://nixos.org/manual/nixos/stable/)). **The release cadence** resembles Fedora rather than Debian. Each stable release gets about seven months of support, so you upgrade twice a year or run `nixos-unstable`. Unstable is the counterpart to Arch, except that a channel moves forward only after Hydra tests pass ([NixOS Wiki: channel branches](https://wiki.nixos.org/wiki/Channel_branches)). **Package breadth** favours Nix: Repology ranks nixpkgs unstable as the largest repository it tracks. Treat that number with care, because it counts projects and nixpkgs includes large auto-generated language package sets. **FHS non-compliance** is the biggest day-to-day friction. NixOS puts only `/bin/sh` and `/usr/bin/env` at standard paths, so `#!/bin/bash` fails. A January 2026 kernel patch changed a build script's shebang to `#!/usr/bin/env bash` for exactly this reason ([LKML](https://lkml.iu.edu/2601.2/01525.html)).

The rough translations are these. AUR or PPA becomes nixpkgs itself, your own derivation or overlay, or NUR (unreviewed, like the AUR) ([NUR](https://github.com/nix-community/NUR)). `apt install` becomes `environment.systemPackages`. `systemctl enable` plus files in `/etc` become NixOS options or `systemd.services.<name>`. stow or chezmoi become Home Manager. asdf, Docker or devcontainers become `nix develop` or `nix-shell` with direnv and nix-direnv, or devenv ([Discourse: dev shells](https://discourse.nixos.org/t/difference-between-nix-shell-nix-shell-nix-develop/32469)). NixOS fits poorly if you need LTS-length support with no twice-yearly upgrade, if you depend heavily on FHS-assuming vendor binaries, if compliance requires a certified distribution, or if nobody on the team can maintain Nix code.

## Recommended start: the generated config first, then a flake when it pays off

There is no official consensus learning path. The official wiki advises getting comfortable with plain NixOS before adding Home Manager or flakes ([wiki.nixos.org](https://wiki.nixos.org/wiki/Main_Page)). The popular community material (the NixOS & Flakes Book, Zero to Nix, Misterio77's templates, Vimjoyer) is flake-first. Forum advice adds that migrating a working `configuration.nix` to a flake is easy, and that you will notice when flakes become useful ([Discourse](https://discourse.nixos.org/t/how-to-start-using-nix-os/37804?page=2)). For an advanced user the defensible path combines the two views. Learn the module system on the generated config, keep it in git from day one, and adopt a flake early, once the basics make sense. Going flake-first from the start (for example with Misterio77's minimal template) is also reasonable if you are comfortable with git. If you do, learn the git-tracking rule in the pitfalls section first.

| Step | What to do | Where |
|---|---|---|
| 1. Orient (about 1 hour) | Read how the store, derivations and the NixOS layers fit together | [How Nix works](https://nixos.org/guides/how-nix-works), [Nix Ecosystem](https://wiki.nixos.org/wiki/Nix_Ecosystem) |
| 2. Try without committing | Ad hoc shells and pinning on your current distro, or NixOS in a VM | [nix.dev First steps](https://nix.dev/tutorials/first-steps/), [NixOS VM tutorial](https://nix.dev/tutorials/nixos/nixos-configuration-on-vm) |
| 3. Learn the language | Attribute sets, `let`, functions, `import`, `inherit` | [Nix language basics](https://nix.dev/tutorials/nix-language), [Nix 1p](https://code.tvl.fyi/about/nix/nix-1p) |
| 4. First real config | Install 26.05; edit `/etc/nixos/configuration.nix`; use `switch`, `test` and rollbacks; read the "Declared in" source of options you use | [NixOS manual](https://nixos.org/manual/nixos/stable/), [option search](https://search.nixos.org/options) |
| 5. Module system | Split into modules with `imports`; learn `mkIf`, `mkDefault`, `mkForce` | [A basic module](https://nix.dev/tutorials/module-system/a-basic-module/), [deep dive](https://nix.dev/tutorials/module-system/deep-dive) |
| 6. Pin: flake or npins | `git init`, then either convert to a flake or pin classically | [Flakes concept](https://nix.dev/concepts/flakes), [wiki Flakes](https://wiki.nixos.org/wiki/Flakes), [npins guide](https://jade.fyi/blog/pinning-nixos-with-npins/) |
| 7. Home Manager (optional) | User dotfiles as a NixOS module, with the branch matched to your release | [HM manual](https://nix-community.github.io/home-manager/), [HM option search](https://home-manager-options.extranix.com/) |
| 8. Tooling | An LSP (nixd or nil), nixfmt, nh | See the tooling table below |
| 9. Go deeper as needed | Overrides, overlays, packaging, secrets, disko, impermanence | [Nixpkgs manual](https://nixos.org/manual/nixpkgs/stable/), [Nix Pills](https://nixos.org/guides/nix-pills/) |
| 10. Stay current | Read the release notes before every upgrade; follow Discourse and NixOS Weekly | [Release notes](https://nixos.org/manual/nixos/stable/release-notes) |

Once you reach step 6, the smallest system flake wraps your existing configuration without rewriting it:

```nix
{
  inputs.nixpkgs.url = "github:NixOS/nixpkgs/nixos-26.05";
  outputs = { self, nixpkgs, ... }: {
    nixosConfigurations.myhost = nixpkgs.lib.nixosSystem {
      modules = [ ./configuration.nix ];
    };
  };
}
# sudo nixos-rebuild switch --flake .#myhost     # nix flake update rewrites flake.lock
```

At step 8, a few declarative settings save trouble later: `nix.gc.automatic`, `nix.optimise.automatic` and a bootloader `configurationLimit` ([wiki: storage optimization](https://wiki.nixos.org/wiki/Storage_optimization)). If you live with downloaded tooling, also set `programs.nix-ld.enable = true` ([wiki: nix-ld](https://wiki.nixos.org/wiki/Nix-ld)). Leave impermanence, disko and multi-host abstractions until you can recover a broken system from the boot menu.

## The links worth bookmarking, by job

On 2026-10-25 every URL below returned HTTP 200, except that reddit.com and nixos.wiki block automated checks. Reach for official sources first, and treat community material as dated: check when something was written and which release it targets.

### Official documentation

| Resource | URL | Use it for |
|---|---|---|
| nixos.org/learn | https://nixos.org/learn/ | Official hub linking every manual and tutorial |
| How Nix works | https://nixos.org/guides/how-nix-works | The 1-hour conceptual orientation |
| NixOS manual (stable) | https://nixos.org/manual/nixos/stable/ | Installation, configuration, upgrades, writing modules, troubleshooting |
| NixOS options appendix | https://nixos.org/manual/nixos/stable/options | Every option for the release, in one page |
| NixOS release notes | https://nixos.org/manual/nixos/stable/release-notes | Renamed or removed options and breaking changes; read before each upgrade |
| nix.dev | https://nix.dev/ | Official tutorials: first steps, language, module system, NixOS VMs, tests, binary caches |
| nix.dev best practices | https://nix.dev/guides/best-practices | Language anti-patterns (`with`, `rec`, `<nixpkgs>`, shallow `//`) |
| nix.dev troubleshooting / FAQ | https://nix.dev/guides/troubleshooting, https://nix.dev/guides/faq | Common errors; running non-Nix binaries |
| Nix reference manual | https://nix.dev/manual/nix/stable/ | Language reference, CLI reference, store internals |
| Nixpkgs manual | https://nixos.org/manual/nixpkgs/stable/ | Overrides, overlays, `lib` functions, language-specific builders |
| Nix Pills | https://nixos.org/guides/nix-pills/ | Low-level derivation internals; read it later, not first |
| Official wiki | https://wiki.nixos.org/ | Hardware pages (NVIDIA, bootloader), Flakes, Home Manager, packaging binaries |
| Wiki: Resources | https://wiki.nixos.org/wiki/Resources | Curated index of books, videos and configs |
| Wiki: NixOS as a desktop | https://wiki.nixos.org/wiki/NixOS_as_a_desktop | Desktop-oriented starting point |

wiki.nixos.org is the **official** wiki, launched in 2024. nixos.wiki is the older, unofficial wiki it forked from, after the original maintainer declined to cooperate ([wiki FAQ](https://wiki.nixos.org/wiki/FAQ)). When a search result points to nixos.wiki, swap the domain.

### Search and lookup

| Tool | URL | Use it for |
|---|---|---|
| Package search | https://search.nixos.org/packages | Attribute names per channel |
| Option search | https://search.nixos.org/options | The first place to check before configuring anything; "Declared in" links to the module source |
| Home Manager option search | https://home-manager-options.extranix.com/ | HM options (official list: https://nix-community.github.io/home-manager/options.xhtml) |
| Noogle | https://noogle.dev/ | Search `lib` and `builtins` functions with docs |
| Nix Package Versions | https://lazamar.co.uk/nix-versions/ | Which nixpkgs revision had an old version of a package |
| MyNixOS | https://mynixos.com/ | Third-party browser for options and packages |
| Searchix / NüschtOS | https://searchix.ovh/, https://github.com/NuschtOS/search | Alternative option and package search |
| nixpkgs source | https://github.com/NixOS/nixpkgs | The ground truth; modules live under `nixos/modules/` |

### Language learning

| Resource | URL | Note |
|---|---|---|
| Nix language basics | https://nix.dev/tutorials/nix-language | The canonical starting tutorial |
| Nix - A One Pager | https://code.tvl.fyi/about/nix/nix-1p | Dense syntax primer for experienced programmers |
| Tour of Nix | https://nixcloud.io/tour/ | Interactive exercises |
| Builtins reference | https://nixos.org/manual/nix/stable/expressions/builtins.html | Every builtin |
| Nixpkgs `lib` reference | https://nixos.org/manual/nixpkgs/stable/#sec-functions-library | `lib.mkIf`, `lib.recursiveUpdate` and the rest |

### Community guides, books and videos

| Resource | URL | Note |
|---|---|---|
| NixOS & Flakes Book (Ryan Yin) | https://nixos-and-flakes.thiscute.world/ | The most complete flake-first NixOS guide; unofficial and opinionated ([Discourse](https://discourse.nixos.org/t/how-can-i-learn-about-flakes/79487)) |
| Zero to Nix (Determinate Systems) | https://zero-to-nix.com/ | Polished Nix-and-flakes intro; little NixOS config content; promotes Determinate tooling |
| Vimjoyer Nix playlist | https://www.youtube.com/playlist?list=PLko9chwSoP-15ZtZxu64k_CuTzXrFpxPE | Short single-topic videos |
| The Nix Hour | https://www.youtube.com/playlist?list=PLyzwHTVJlRc8yjlx4VR4LU5A5O44og9in | Weekly in-depth Q&A sessions |
| Nix from First Principles: Flake Edition | https://tonyfinn.com/blog/nix-from-first-principles-flake-edition/ | Concept-driven flake explanation |
| How to Learn Nix (Ian Henry) | https://ianthehenry.com/posts/how-to-learn-nix/ | A candid long-form learning diary |
| Wombat's Book of Nix | https://mhwombat.codeberg.page/nix-book/ | Gentle book-length introduction |
| NixOS Asia tutorials | https://nixos.asia/en/tutorial | Practical tutorials |
| NixOS in Production | https://leanpub.com/nixos-in-production | Server and deployment perspective |
| awesome-nix | https://github.com/nix-community/awesome-nix | Curated master list |

### Example configs and templates

Read these for patterns. Do not adopt them wholesale.

| Resource | URL | Note |
|---|---|---|
| Misterio77/nix-starter-configs | https://github.com/Misterio77/nix-starter-configs | "minimal" (NixOS + HM) and "standard" flake templates; the README warns it may lag |
| ryan4yin/nix-config | https://github.com/ryan4yin/nix-config | Config of the Flakes Book author |
| Misterio77/nix-config | https://github.com/Misterio77/nix-config | Multi-host reference |
| mitchellh/nixos-config | https://github.com/mitchellh/nixos-config | VM-centric dev workstation setup |
| Wiki: Configuration Collection | https://wiki.nixos.org/wiki/Configuration_Collection | Index of public configs |
| Wiki: Comparison of NixOS setups | https://wiki.nixos.org/wiki/Comparison_of_NixOS_setups | Shows how different people structure configs |

### Tooling to know early

| Tool | URL | Why |
|---|---|---|
| nixd / nil | https://github.com/nix-community/nixd, https://github.com/oxalica/nil | LSPs; nixd offers option-aware completion. Avoid the older rnix-lsp |
| nixfmt | https://github.com/NixOS/nixfmt | The official formatter (RFC 166); `pkgs.nixfmt` |
| nh | https://github.com/nix-community/nh | `nh os switch` shows a build tree, a diff and a confirmation prompt; `nh clean` handles retention; `nh search`; works with flakes and classic configs; `programs.nh.enable` ([nh README](https://github.com/nix-community/nh)) |
| nix-output-monitor, nvd, nix-tree | https://github.com/maralorn/nix-output-monitor, https://git.sr.ht/~khumba/nvd, https://github.com/utdemir/nix-tree | Build output, generation diffs, closure browsing |
| npins | https://github.com/andir/npins | Pinning without flakes |
| sops-nix / agenix | https://github.com/Mic92/sops-nix, https://github.com/ryantm/agenix | Secrets kept out of the world-readable store |
| disko / nixos-anywhere / impermanence | https://github.com/nix-community/disko, https://github.com/nix-community/nixos-anywhere, https://github.com/nix-community/impermanence | Declarative disks, installs over SSH, ephemeral root; for later |

### Community and news

| Channel | URL | Note |
|---|---|---|
| Discourse | https://discourse.nixos.org/ | Official forum; the best place for searchable answers |
| Matrix space | https://matrix.to/#/#space:nixos.org | Official real-time chat |
| NixOS Weekly | https://weekly.nixos.org/ | Newsletter |
| Planet NixOS | http://planet.nixos.org/ | Blog aggregator (nixpkgs.news has been inactive since July 2024) |
| r/NixOS | https://www.reddit.com/r/NixOS/ | Active but unofficial; not listed on [nixos.org/community](https://nixos.org/community/) |
| NixCon 2026 | https://2026.nixcon.org/ | Conference talks (Kraków, September 2026) |

## Ten pitfalls that eat newcomers' weekends

Most of these come from Debian or Arch reflexes meeting a declarative system. A 2020 Discourse thread by a NixOS team member, "New users are using NixOS wrong, and it's our fault", named the root causes still seen today. New users install with `nix-env` (which the manual once recommended), create users with `useradd` and edit sudoers with `visudo`, and miss that `configuration.nix` is meant to keep being edited after installation ([Discourse #9973](https://discourse.nixos.org/t/new-users-are-using-nixos-wrong-and-its-our-fault/9973)).

| Pitfall | Symptom | Fix |
|---|---|---|
| **Flake cannot see a new file** | "No such file or directory" or "path does not exist" for a file that clearly exists | Flakes copy only git-tracked files. Run `git add` (staging is enough; `git add -N` works). A `.gitignore`d `hardware-configuration.nix` needs `git add -f` ([Discourse](https://discourse.nixos.org/t/nix-flakes-nix-store-source-no-such-file-or-directory/17836/26)). "Git tree is dirty" is only a warning |
| **Downloaded binary will not run** | "cannot execute: required file not found" | No `/lib64/ld-linux-x86-64.so.2`. Order of preference: the nixpkgs package, then packaging it with `autoPatchelfHook` (`buildFHSEnv` as a last resort), then `steam-run`, or enable `programs.nix-ld` and log out and back in ([nix.dev FAQ](https://nix.dev/guides/faq); [wiki: Packaging/Binaries](https://wiki.nixos.org/wiki/Packaging/Binaries)). This bites pip wheels, npm binaries, uv Pythons and editor-downloaded language servers |
| **Imperative installs** | Packages and settings drift, then vanish or conflict | Declare them in config. Use `nix-shell -p` / `nix shell` for one-offs. Treat `nix-env -i` and `nix profile install` as experiments only |
| **Bumping `system.stateVersion`** | Unexpected service behaviour, possible data loss | It records the *first-install* release and "should never be updated" unless the release notes say so. Upgrading means changing the channel or flake input ([wiki FAQ](https://wiki.nixos.org/wiki/FAQ/When_do_I_update_stateVersion)). The same goes for `home.stateVersion` |
| **Store and `/boot` fill up** | "No space left" during `nixos-rebuild` | Generations are GC roots. Set `nix.gc.automatic` with `--delete-older-than 30d`, `nix.optimise.automatic`, and run GC with `sudo` to clear system generations ([wiki](https://wiki.nixos.org/wiki/Storage_optimization)). `boot.loader.systemd-boot.configurationLimit` defaults to unlimited, and even a 1 GiB ESP has filled up ([Discourse](https://discourse.nixos.org/t/second-generation-fills-up-1-gib-boot-partition/67968)). Size the ESP generously |
| **Stale docs and LLM answers** | Options that do not exist or were renamed | `hardware.opengl` became `hardware.graphics` in 24.11 ([Discourse](https://discourse.nixos.org/t/24-11-broke-opengl-for-me/57497)). LLMs "hallucinat[e] package names from 2019" ([Discourse](https://discourse.nixos.org/t/local-ai-agent-for-nixos-configuration-looking-for-experience-reports/77238)). Check every option on search.nixos.org for *your* release, and read evaluation warnings |
| **Infinite recursion** | "infinite recursion encountered" | Imports are resolved before config, so never make `imports` depend on `config`. Import unconditionally and gate with `lib.mkIf` ([Discourse](https://discourse.nixos.org/t/infinite-recursion-on-optional-import/8892)). Avoid `rec` self-shadowing and top-level `with`, and use `lib.recursiveUpdate` instead of the shallow `//` ([nix.dev best practices](https://nix.dev/guides/best-practices)) |
| **Home Manager mismatch and collisions** | Version warning; activation fails because a dotfile already exists | Match the branch to Nixpkgs ([wiki](https://wiki.nixos.org/wiki/Home-manager)). Set `home-manager.backupFileExtension`, but note that a second collision with an existing `.backup` fails again ([Discourse](https://discourse.nixos.org/t/nixos-rebuild-fails-on-backup-up-config-file-by-home-manager/45992)). Choose standalone or module per user, not both |
| **Mixing stable and unstable** | GL context failures, `GLIBC_2.38 not found` | Pass a separate unstable Nixpkgs through `specialArgs` for specific packages. Do not override `pkgs`. GUI and GPU apps are the risky case ([Discourse](https://discourse.nixos.org/t/mixing-stable-and-unstable-packages-on-flake-based-nixos-system/50351/4.md)) |
| **Secrets in the store** | Passwords and tokens readable by every user | "All files in the Nix store are readable by any system user" ([agenix](https://git.rgbcu.be/RGBCube/agenix/src/tag/0.9/README.md)). Use sops-nix or agenix, or options that take a `*File` path |

Three more are worth a line each. On NVIDIA you need `nixpkgs.config.allowUnfree` even with the open kernel modules, an explicit `hardware.nvidia.open` choice (mandatory since driver 560), `hardware.graphics.enable`, and PRIME bus IDs converted to decimal ([wiki: NVIDIA](https://wiki.nixos.org/wiki/NVIDIA)). For remote or network changes, use `nixos-rebuild test`: a reboot reverts it. Remember that `build-vm` does not prove the config boots on real hardware ([nixos-rebuild man page](https://www.mankier.com/8/nixos-rebuild)). Finally, do not copy someone's whole config. Copied configs carry machine-specific swap, disk and secure-boot settings that break on your hardware ([Discourse](https://discourse.nixos.org/t/new-to-nixos-should-i-install-it-or-not/78827)), and impermanence in particular has a steep learning curve with many edge cases ([Lemmy](https://lemmy.uninsane.org/post/25586)). Avoid making your primary laptop your first install if you cannot afford some downtime.

## Conclusion

For an advanced Linux user, the hard part of NixOS is not Linux. It is learning to think in terms of evaluation instead of mutation. Most of the frustration traced above comes from treating `/etc`, `PATH` or the release number as places to make changes, when NixOS treats them as outputs. Once that sinks in, the "experimental" flakes label matters less than it seems. It is a governance question, not a reliability one, and the practical decision is just when to start pinning. The boot-menu rollback also makes experimenting unusually cheap, as long as you keep a few generations and test risky changes with `nixos-rebuild test`.

The ecosystem changes quickly. Options get renamed, stage 1 moved to systemd in 26.05, and 26.11 is due within weeks of this report. So the most useful resources are live sources that track your release: search.nixos.org, the release notes, the nixpkgs source behind each option, and Discourse. Tutorials, starter templates and LLM answers are a snapshot of whatever release they were written for. Use them for patterns, and check each option name against your own release before you rely on it.

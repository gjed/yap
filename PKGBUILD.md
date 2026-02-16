<!-- # The PKGBUILD -->

Yap adopts the [PKGBUILD](https://wiki.archlinux.org/title/PKGBUILD) format
from Arch Linux as its single package specification. One PKGBUILD produces
`.deb`, `.rpm`, `.pkg.tar.zst`, or `.apk` packages depending on the target
distribution.

## Why PKGBUILD

Most packaging systems require distribution-specific spec files -- a `.spec`
for RPM, `debian/` directory trees for deb, `APKBUILD` for Alpine, and so on.
Maintaining these in parallel for the same software is repetitive and
error-prone.

PKGBUILD solves this by providing a minimal, readable format that describes
**what** to build and **how**, without tying you to a single package manager:

- **One file, all distros** -- a single PKGBUILD replaces multiple spec formats.
- **Simple shell syntax** -- variables, arrays, and functions. No DSL to learn.
- **Directives for differences** -- where distros diverge (dependency names,
  paths), append `__<directive>` to override per target instead of maintaining
  separate files.
- **Battle-tested** -- the format powers the entire Arch User Repository (AUR)
  with tens of thousands of packages.

## How Yap Extends It

Yap is compatible with the upstream PKGBUILD format and adds a few things on
top:

- **Directives** -- target-specific overrides (`depends__apt`, `depends__yum`,
  `pkgdesc__ubuntu_noble`). See [Directives](Directives).
- **Cross-distro scriptlets** -- `preinst()`, `postinst()`, `prerm()`,
  `postrm()` work across deb, rpm, and pacman. RPM also supports `pretrans()`
  and `posttrans()`.
- **Embedded interpreter** -- Yap parses and executes PKGBUILDs with a built-in
  shell interpreter. Bash is not required on the build host.
- **`sha256sums` / `sha512sums`** -- hash type is inferred from the length of
  the hex string (64 or 128 characters).
- **Custom variables, arrays, and helper functions** *(since v1.48)* --
  user-defined variables and arrays are automatically available in all build
  functions. Custom functions (any function not recognized as a standard
  PKGBUILD field) are treated as helpers and injected into build scripts.
  Helper functions referenced by install scriptlets (`preinst`, `postinst`,
  etc.) are automatically included in the scriptlet with transitive dependency
  resolution.

## Subsections

- [Format](Format) -- PKGBUILD syntax (strings, arrays, functions)
- [Spec File](Spec-file-‐-the-PKGBUILD) -- Complete field and function reference
- [Variables](Variables) -- Built-in variables, custom variables, and helper functions
- [Directives](Directives) -- Distro-specific overrides

## Further Reading

- [Arch Wiki -- PKGBUILD](https://wiki.archlinux.org/title/PKGBUILD)
- [Arch Wiki -- Creating packages](https://wiki.archlinux.org/title/Creating_packages)

# Yap - Yet Another Packager

Yap builds `.deb`, `.rpm`, `.pkg.tar.zst`, and `.apk` packages from a single
PKGBUILD specification. It uses Arch Linux's PKGBUILD format and runs on any
Linux distribution.

## Installation

```sh
wget https://github.com/M0Rf30/yap/releases/latest/download/yap_Linux_x86_64.tar.gz
tar -xvf yap_Linux_x86_64.tar.gz
sudo mv yap /usr/local/bin/
```

## Quick Start

1. Create a project directory with a `yap.json` and a subdirectory containing
   a `PKGBUILD`:

   ```text
   myproject/
   ├── yap.json
   └── mypackage/
       └── PKGBUILD
   ```

2. Build packages:

   ```sh
   # Build for a specific distro
   yap build ubuntu-noble /path/to/myproject

   # Auto-detect distro from the current system
   yap build /path/to/myproject
   ```

3. Built packages are placed in the output directory defined in `yap.json`.

## Wiki Pages

- [CLI](CLI) -- Commands, flags, and build targets
- [The PKGBUILD](PKGBUILD) -- Format introduction, syntax, fields, variables, and directives
- [Project File](Project-File) -- yap.json purpose and format

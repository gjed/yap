<!-- # CLI -->

## Commands

| Command | Description |
| --- | --- |
| `yap build [distro] <path>` | Build packages from a project or PKGBUILD |
| `yap pull [distro]` | Pull the OCI container image for a distro |
| `yap prepare [distro]` | Install base development packages |
| `yap list-distros` | List available build targets |
| `yap zap [distro] [path]` | Deep clean the build environment |
| `yap completion <shell>` | Generate shell completions (bash, zsh, fish) |
| `yap version` | Print version |

## Build Flags

| Flag | Short | Description |
| --- | --- | --- |
| `--cleanbuild` | `-c` | Remove `$srcdir/` before building |
| `--nomakedeps` | `-d` | Skip makedeps checks |
| `--nobuild` | `-o` | Download and extract sources only |
| `--pkgver` | `-w` | Override package version |
| `--pkgrel` | `-r` | Override package release |
| `--skip-sync` | `-s` | Skip package manager sync |
| `--ssh-password` | `-p` | SSH password for private Git repos |
| `--from` | | Build starting from a specific package |
| `--to` | | Build until a specific package |
| `--zap` | `-z` | Remove entire staging dir before building |

## Usage

Build for a specific distribution:

```sh
yap build ubuntu-noble /path/to/project
```

Auto-detect the distribution from the current system:

```sh
yap build /path/to/project
```

Install base development packages before building:

```sh
yap prepare ubuntu-noble
```

Pull a pre-built container image and build inside it:

```sh
yap pull ubuntu-noble
```

## Subsections

- [Build Targets](Build-Targets) -- Supported distributions
- [Containers](Containers) -- OCI container images for building packages

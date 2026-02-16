<!-- # Directives -->

Directives apply variable values to a specific subset of build targets. Append
`__<directive>` to any variable or array name.

All variables and arrays support directives, including user-defined ones.

## Priority

When multiple directives match, the most specific one wins:

| Priority | Level | Example |
| --- | --- | --- |
| 1 (lowest) | Package manager | `depends__apt` |
| 2 | Distribution | `depends__ubuntu` |
| 3 (highest) | Distribution release | `depends__ubuntu_noble` |

A variable without a directive has priority 0 and is used as the default.

## Package Manager Directives

| Directive | Applies to |
| --- | --- |
| `apk` | All APK packages (Alpine) |
| `apt` | All DEB packages (Debian, Ubuntu, Linux Mint, Pop!\_OS) |
| `pacman` | All PKG packages (Arch) |
| `yum` | All RPM packages (Fedora, Rocky, CentOS, RHEL, Amazon, Oracle, AlmaLinux) |
| `zypper` | All RPM packages (openSUSE) |

## Distribution Directives

| Directive | Applies to |
| --- | --- |
| `almalinux` | All AlmaLinux releases |
| `alpine` | All Alpine Linux releases |
| `amazon` | All Amazon Linux releases |
| `arch` | All Arch Linux releases |
| `centos` | All CentOS releases |
| `debian` | All Debian releases |
| `fedora` | All Fedora releases |
| `linuxmint` | All Linux Mint releases |
| `opensuse_leap` | All openSUSE Leap releases |
| `oracle` | All Oracle Linux releases |
| `pop` | All Pop!\_OS releases |
| `rhel` | All RHEL releases |
| `rocky` | All Rocky Linux releases |
| `ubuntu` | All Ubuntu releases |

## Release Directives

Use `<distro>_<codename>` for release-specific values:

| Directive | Applies to |
| --- | --- |
| `amazon_1` | Amazon Linux 1 |
| `amazon_2` | Amazon Linux 2 |
| `debian_jessie` | Debian Jessie |
| `debian_stretch` | Debian Stretch |
| `debian_buster` | Debian Buster |
| `fedora_38` | Fedora 38 |
| `rocky_8` | Rocky Linux 8 |
| `rocky_9` | Rocky Linux 9 |
| `rocky_10` | Rocky Linux 10 |
| `ubuntu_bionic` | Ubuntu 18.04 Bionic |
| `ubuntu_focal` | Ubuntu 20.04 Focal |
| `ubuntu_jammy` | Ubuntu 22.04 Jammy |
| `ubuntu_noble` | Ubuntu 24.04 Noble |

## Example

```sh
pkgdesc="My application"
pkgdesc__ubuntu="My application for Ubuntu"
pkgdesc__ubuntu_noble="My application for Ubuntu Noble"

depends=(
  'libssl'
)
depends__apt=(
  'libssl-dev'
)
depends__yum=(
  'openssl-devel'
)

makedepends__alpine=(
  'build-base'
)
makedepends__apt=(
  'build-essential'
)
```

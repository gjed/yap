<!-- # Build Targets -->

Pass a build target to [`yap build`](CLI) to specify the distribution. Use a
generic target to build for the default release, or a specific target with a
release name or version.

```sh
yap build <target> /path/to/project
```

Run `yap list-distros` to list all available targets.

## Generic Targets

| Target | Distribution | Package Format |
| --- | --- | --- |
| `almalinux` | AlmaLinux | `.rpm` |
| `alpine` | Alpine Linux | `.apk` |
| `amzn` | Amazon Linux | `.rpm` |
| `arch` | Arch Linux | `.pkg.tar.zst` |
| `centos` | CentOS | `.rpm` |
| `debian` | Debian | `.deb` |
| `fedora` | Fedora | `.rpm` |
| `linuxmint` | Linux Mint | `.deb` |
| `opensuse-leap` | openSUSE Leap | `.rpm` |
| `ol` | Oracle Linux | `.rpm` |
| `pop` | Pop!\_OS | `.deb` |
| `rhel` | Red Hat Enterprise Linux | `.rpm` |
| `rocky` | Rocky Linux | `.rpm` |
| `ubuntu` | Ubuntu | `.deb` |

## Specific Targets

| Target | Release |
| --- | --- |
| `amazon-1` | Amazon Linux 1 |
| `amazon-2` | Amazon Linux 2 |
| `debian-jessie` | Debian 8 Jessie |
| `debian-stretch` | Debian 9 Stretch |
| `debian-buster` | Debian 10 Buster |
| `fedora-38` | Fedora 38 |
| `rocky-8` | Rocky Linux 8 |
| `rocky-9` | Rocky Linux 9 |
| `rocky-10` | Rocky Linux 10 |
| `ubuntu-bionic` | Ubuntu 18.04 Bionic |
| `ubuntu-focal` | Ubuntu 20.04 Focal |
| `ubuntu-jammy` | Ubuntu 22.04 Jammy |
| `ubuntu-noble` | Ubuntu 24.04 Noble |

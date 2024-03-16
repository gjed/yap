Directives are used to specify variables that only apply to a limited set of
build targets.

All variables can use directives including user defined variables.

To use directives include the directive after a variable separated by a colon
such as `pkgdesc__ubuntu="This description will only apply to Ubuntu packages"`.

The directives above are sorted from lowest to the highest priority.

| directive        | value                     |
|------------------|---------------------------|
| `apk`            | all apk packages          |
| `apt`            | all deb packages          |
| `pacman`         | all pkg packages          |
| `yum`            | all yum rpm packages      |
| `alpine`         | all Alpine Linux packages |
| `arch`           | all Arch Linux releases   |
| `amazon`         | all Amazon Linux releases |
| `centos`         | all CentOS releases       |
| `debian`         | all Debian releases       |
| `fedora`         | all Fedora releases       |
| `oracle`         | all Oracle Linux releases |
| `ubuntu`         | all Ubuntu releases       |
| `amazon_1`       | Amazon Linux 1            |
| `amazon_2`       | Amazon Linux 2            |
| `debian_jessie`  | Debian Jessie             |
| `debian_stretch` | Debian Stretch            |
| `debian_buster`  | Debian Buster             |
| `fedora_38`      | Fedora 38                 |
| `rocky_8`        | Rocky Linux 8             |
| `rocky_9`        | Rocky Linux 9             |
| `ubuntu_bionic`  | Ubuntu Bionic             |
| `ubuntu_focal`   | Ubuntu Focal              |
| `ubuntu_jammy`   | Ubuntu Jammy              |
# Spec File - the PKGBUILD

Complete reference of all supported fields and functions.
See [The PKGBUILD](PKGBUILD) for an introduction to the format.

## Variables

| Key | Type | Description |
| --- | --- | --- |
| `pkgname` | `string` | Package name (required) |
| `pkgver` | `string` | Package version (required) |
| `pkgrel` | `string` | Package release number (required) |
| `epoch` | `string` | Package epoch, used to force upgrade over a lower version number |
| `pkgdesc` | `string` | Short package description (required) |
| `maintainer` | `string` | Package maintainer name and email |
| `url` | `string` | Upstream project URL |
| `section` | `string` | Package section (Debian only). Available: `admin` `comm` `database` `debug` `devel` `doc` `editors` `electronics` `embedded` `fonts` `games` `graphics` `httpd` `interpreters` `kernel` `libdevel` `libs` `localization` `mail` `math` `misc` `net` `news` `science` `shells` `sound` `text` `vcs` `video` `web` `x11` |
| `priority` | `string` | Package priority (Debian only) |
| `install` | `string` | Name of the install scriptlet file |
| `debconf_config` | `string` | Debconf config file (Debian only) |
| `debconf_template` | `string` | Debconf template file (Debian only) |

## Arrays

| Key | Type | Description |
| --- | --- | --- |
| `arch` | `list` | Supported architectures. Use `any` for arch-independent packages. Values: `x86_64`, `i686`, `aarch64`, `armv7h`, etc. |
| `license` | `list` | SPDX license identifiers (e.g., `GPL-3.0-only`, `MIT`). Also accepts `PROPRIETARY` and `CUSTOM` |
| `copyright` | `list` | Copyright statements |
| `depends` | `list` | Runtime dependencies |
| `optdepends` | `list` | Optional dependencies |
| `makedepends` | `list` | Build-time dependencies |
| `provides` | `list` | Virtual packages this package provides |
| `conflicts` | `list` | Packages that conflict with this one |
| `replaces` | `list` | Packages this one replaces |
| `source` | `list` | Source URIs or local paths relative to the PKGBUILD. Supports HTTP, HTTPS, FTP, Git (`git+https://...`), and local files. Use `filename::url` to set a custom filename |
| `sha256sums` | `list` | SHA-256 checksums for sources. Use `SKIP` to bypass verification |
| `sha512sums` | `list` | SHA-512 checksums for sources. Use `SKIP` to bypass verification |
| `backup` | `list` | Config files that should not be overwritten on upgrade (absolute paths without leading `/`) |
| `options` | `list` | Build options. `!strip` disables binary stripping, `!staticlibs` disables static library processing |

## Functions

| Key | Type | Description |
| --- | --- | --- |
| `prepare()` | `func` | Runs before `build()`. Use for patching sources |
| `build()` | `func` | Build the source. Working directory is `$srcdir` |
| `package()` | `func` | Install files into `$pkgdir`. Working directory is `$srcdir` (required) |
| `preinst()` | `func` | Runs before package installation |
| `postinst()` | `func` | Runs after package installation |
| `prerm()` | `func` | Runs before package removal |
| `postrm()` | `func` | Runs after package removal |
| `pretrans()` | `func` | Runs at the start of a transaction (RPM only) |
| `posttrans()` | `func` | Runs at the end of a transaction (RPM only) |

## Source Types

| Type | Syntax | Example |
| --- | --- | --- |
| HTTP/HTTPS | `https://example.com/file.tar.gz` | `"https://example.com/v1.0.tar.gz"` |
| FTP | `ftp://example.com/file.tar.gz` | `"ftp://mirror.example.com/src.tar.gz"` |
| Git | `git+https://...` | `"git+https://github.com/user/repo"` |
| Git branch | `git+https://...#branch=name` | `"git+https://github.com/user/repo#branch=dev"` |
| Git tag | `git+https://...#tag=name` | `"git+https://github.com/user/repo#tag=v1.0"` |
| Local file | relative path | `"my-config.conf"` |
| Custom name | `filename::url` | `"source.tar.gz::https://example.com/v1.tar.gz"` |

## Example

```sh
pkgname=myapp
pkgver=1.0
pkgrel=1
pkgdesc="My application"
maintainer="John Doe <john@example.com>"
arch=('x86_64')
license=('MIT')
url="https://github.com/user/myapp"
depends=(
  'libc'
)
makedepends=(
  'gcc'
  'make'
)
makedepends__apt=(
  'build-essential'
)
source=(
  "git+${url}#tag=v${pkgver}"
)
sha256sums=(
  'SKIP'
)

build() {
  cd "${srcdir}/${pkgname}"
  make
}

package() {
  cd "${srcdir}/${pkgname}"
  make DESTDIR="${pkgdir}" install
}
```

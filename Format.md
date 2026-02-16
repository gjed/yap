<!-- # PKGBUILD Format -->

Syntax reference for writing PKGBUILDs.
See [The PKGBUILD](PKGBUILD) for an introduction to the format.

## Strings

```sh
pkgname="mypackage"
pkgdesc=`string with "quotes" inside`
```

## Variable Expansion

```sh
url="https://github.com/user/${pkgname}"
```

## Arrays

```sh
# Single element
arch=('x86_64')

# Multiple elements
depends=(
  'libfoo'
  'libbar'
)
```

## Functions

```sh
build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
}
```

## Directives

Append `__<directive>` to any variable or array to make it target-specific:

```sh
pkgdesc="Default description"
pkgdesc__ubuntu="Ubuntu-specific description"

makedepends=(
  'gcc'
)
makedepends__apt=(
  'build-essential'
)
```

See [Directives](Directives) for the full list.

# Variables

## Built-in Variables

These variables are set automatically during the build and available in
`prepare()`, `build()`, and `package()` functions.

### Directory Variables

| Variable | Description |
| --- | --- |
| `$srcdir` | Source directory where all sources are downloaded and extracted |
| `$pkgdir` | Package root directory. Install files here in `package()` |
| `$startdir` | Directory containing the PKGBUILD |

### Package Metadata

The following PKGBUILD fields are also exported as environment variables:

| Variable | Description |
| --- | --- |
| `$pkgname` | Package name |
| `$pkgver` | Package version |
| `$pkgrel` | Package release number |
| `$epoch` | Package epoch |
| `$maintainer` | Package maintainer |
| `$url` | Upstream URL |

## Custom Variables *(since v1.48)*

Any variable in the PKGBUILD that is not a recognized field is treated as a
custom variable. Custom variables are exported as environment variables and
available in all functions.

```sh
_buildflags="-O2 -Wall"
_srcname="${pkgname}-${pkgver}"

build() {
  cd "${srcdir}/${_srcname}"
  CFLAGS="${_buildflags}" make
}
```

Custom arrays work the same way:

```sh
_patches=(
  'fix-build.patch'
  'add-feature.patch'
)

prepare() {
  cd "${srcdir}/${_srcname}"
  for p in "${_patches[@]}"; do
    patch -Np1 -i "${srcdir}/${p}"
  done
}
```

## Helper Functions *(since v1.48)*

Any function not recognized as a standard PKGBUILD function (`build`,
`package`, `prepare`, `preinst`, `postinst`, `prerm`, `postrm`, `pretrans`,
`posttrans`) is treated as a helper function.

Helper functions are injected into build scripts automatically:

```sh
_install_license() {
  install -Dm 644 -t "${pkgdir}/usr/share/licenses/${pkgname}" LICENSE
}

package() {
  cd "${srcdir}/${_srcname}"
  make DESTDIR="${pkgdir}" install
  _install_license
}
```

Helper functions referenced by install scriptlets (`preinst`, `postinst`, etc.)
are also included automatically, with transitive dependency resolution -- if
helper A calls helper B, both are injected.

## Usage

```sh
build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  ./configure --prefix=/usr
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
}
```

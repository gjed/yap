<!-- # Project File (yap.json) -->

The `yap.json` file defines a multi-package build project. It tells yap which
packages to build, in what order, and where to put the output.

For single-package builds, `yap.json` is optional -- yap can operate directly
on a directory containing a PKGBUILD.

## Format

```json
{
  "name": "My Project",
  "description": "Project description",
  "buildDir": "/tmp",
  "output": "artifacts",
  "projects": [
    { "name": "libfoo", "install": true },
    { "name": "myapp" }
  ]
}
```

## Fields

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `name` | string | yes | Project name |
| `description` | string | yes | Project description |
| `buildDir` | string | yes | Working directory for builds |
| `output` | string | yes | Directory where built packages are placed |
| `projects` | array | yes | Ordered list of packages to build |

### Project Entry

Each entry in the `projects` array corresponds to a subdirectory containing a
PKGBUILD.

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `name` | string | yes | Subdirectory name containing the PKGBUILD. Must not start with `.` or `./` |
| `install` | bool | no | Install the package after building (default: `false`) |

## Build Order and Dependencies

Packages are built sequentially in the order listed in `projects`. Set
`"install": true` on a package to install it immediately after building, making
it available as a build dependency for subsequent packages.

```json
{
  "projects": [
    { "name": "libfoo", "install": true },
    { "name": "libbar", "install": true },
    { "name": "myapp" }
  ]
}
```

In this example, `libfoo` is built and installed first, then `libbar` (which
may depend on `libfoo`), then `myapp` (which may depend on both).

## Partial Builds

Use the `--from` and `--to` flags to build a subset of packages:

```sh
# Build only libbar and myapp
yap build ubuntu-noble /path/to/project --from libbar

# Build only libfoo and libbar
yap build ubuntu-noble /path/to/project --to libbar
```

## Directory Layout

```text
myproject/
├── yap.json
├── libfoo/
│   └── PKGBUILD
├── libbar/
│   └── PKGBUILD
└── myapp/
    └── PKGBUILD
```

<!-- # Containers -->

Yap provides pre-built OCI container images with everything needed to build
packages for a given distribution. The images work with both Docker and Podman.

## Available Images

Images are published to Docker Hub as `m0rf30/yap-<target>`:

| Image | Distribution |
| --- | --- |
| `m0rf30/yap-alpine` | Alpine Linux |
| `m0rf30/yap-arch` | Arch Linux |
| `m0rf30/yap-rocky-8` | Rocky Linux 8 |
| `m0rf30/yap-rocky-9` | Rocky Linux 9 |
| `m0rf30/yap-rocky-10` | Rocky Linux 10 |
| `m0rf30/yap-ubuntu-focal` | Ubuntu 20.04 Focal |
| `m0rf30/yap-ubuntu-jammy` | Ubuntu 22.04 Jammy |
| `m0rf30/yap-ubuntu-noble` | Ubuntu 24.04 Noble |

## Pulling Images

Use `yap pull` to download an image:

```sh
yap pull ubuntu-noble
```

This detects the container runtime automatically (Podman is preferred over
Docker) and runs the equivalent of:

```sh
podman pull docker.io/m0rf30/yap-ubuntu-noble
```

## Building Inside a Container

Each image has `yap` as its entrypoint. Mount your project directory and pass
the build arguments:

```sh
docker run --rm -v /path/to/project:/project \
  m0rf30/yap-ubuntu-noble build ubuntu-noble /project
```

Or with Podman:

```sh
podman run --rm -v /path/to/project:/project \
  m0rf30/yap-ubuntu-noble build ubuntu-noble /project
```

Built packages are written to the output directory defined in
[yap.json](Project-File), so mount or copy that path to retrieve them.

## Image Contents

Each image is a multi-stage build that includes:

- The `yap` binary (statically compiled, compressed with UPX)
- Base development toolchain for the target distribution
- Go toolchain
- Bash completions for `yap`

The images do not include your project sources -- mount them at runtime.

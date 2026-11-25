# Portainer: ReadyStack build kit

The offline build kit for the Docker image `readystack/portainer:2.45.4-CE-ubuntu24.04-r1`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [2.45.4-CE-ubuntu24.04-r1](https://github.com/readystack-dev/portainer/releases/tag/2.45.4-CE-ubuntu24.04-r1)
- Image: [`docker.io/readystack/portainer:2.45.4-CE-ubuntu24.04-r1`](https://hub.docker.com/r/readystack/portainer/tags), manifest digest `sha256:1812f46cdac0a4763b59fe067962c956b3ccf1ea0098939fc39c9ffdd9e809f1`
- Product page: https://readystack.dev/products/portainer
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=portainer

Portainer is distributed under its upstream licence (Zlib); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [2.45.4-CE-ubuntu24.04-r1 release](https://github.com/readystack-dev/portainer/releases/tag/2.45.4-CE-ubuntu24.04-r1): `ReadyStack-portainer-2.45.4-CE-ubuntu24.04-r1.tar.gz` (468.5 MB), SHA-256 `90b1a3127b1b6a601ad3068151870d9b463f347718f54287e14c98e26a6dc4f6`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-portainer-2.45.4-CE-ubuntu24.04-r1.rebuild.json.sigstore ReadyStack-portainer-2.45.4-CE-ubuntu24.04-r1.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-portainer-2.45.4-CE-ubuntu24.04-r1.tar.gz
cd 2.45.4-CE-ubuntu24.04-r1
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-portainer-2.45.4-CE-ubuntu24.04-r1.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/portainer/recipe. The complete kit is the release download. Each release is a tag here.

[![ReadyStack](https://readystack.dev/logo.svg)](https://readystack.dev)

**Stable, Open-source Releases, Automated** · [readystack.dev](https://readystack.dev)

[![Docker Hub](https://img.shields.io/badge/Docker%20Hub-readystack%2Fportainer-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/readystack/portainer) [![Docker pulls](https://img.shields.io/docker/pulls/readystack/portainer)](https://hub.docker.com/r/readystack/portainer) [![Grade at release](https://img.shields.io/badge/grade%20at%20release-A%20%2894%25%29-2ea44f)](https://readystack.dev/products/portainer) [![Signed: cosign](https://img.shields.io/badge/signed-cosign-2ea44f)](https://readystack.dev/keys/cosign.pub) ![SBOM: SPDX](https://img.shields.io/badge/SBOM-SPDX-2ea44f) ![Provenance: SLSA v1](https://img.shields.io/badge/provenance-SLSA%20v1-2ea44f) ![Offline rebuild: verified](https://img.shields.io/badge/offline%20rebuild-verified-2ea44f)

# Portainer: ReadyStack build kit

The offline build kit for the Docker image `readystack/portainer:2.45.4-CE-ubuntu24.04-r1`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [2.45.4-CE-ubuntu24.04-r1](https://github.com/readystack-dev/portainer/releases/tag/2.45.4-CE-ubuntu24.04-r1)
- Image: [`docker.io/readystack/portainer:2.45.4-CE-ubuntu24.04-r1`](https://hub.docker.com/r/readystack/portainer/tags), manifest digest `sha256:1812f46cdac0a4763b59fe067962c956b3ccf1ea0098939fc39c9ffdd9e809f1`
- Product page: https://readystack.dev/products/portainer
- Source and build recipe: https://readystack.dev/products/portainer/recipe
- Build trail: https://readystack.dev/products/portainer/trail/2.45.4-CE-ubuntu24.04-r1
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=portainer

## The image

Single container, one static CGO-free Go binary (`portainer`) that serves a web UI + a REST API + an Edge reverse-tunnel server, all in one foreground process. Portainer is a container-management GUI for Docker / Docker Swarm / Kubernetes. ALL state - users, environments, stacks, settings, edge configs - lives in an EMBEDDED bbolt key-value database at /data/portainer.db that the server creates + migrates itself; NO external/relational DB, NO docker-compose, NO sidecar. The on-disk web frontend (dist/public) is served from /opt/portainer/public. The image IS the complete running instance.

## Who uses Portainer and why

Homelab operators, hobbyists, students and anyone experimenting with containers on their own hardware.

Portainer Community Edition is a free, lightweight web interface for managing containers on container hosts and Kubernetes.

A typical use: A hobbyist runs many self-hosted apps on a home server and loses track of them on the command line. Portainer shows every container on one web page, where they view its logs and statistics, open its console, and edit or remove it with a few clicks.

From the upstream project's own description: https://github.com/portainer/portainer, https://docs.portainer.io/user/docker/containers.

## This release

- Docker Scout policy grade at release: **A** (94%), graded 2026-11-22 with `docker scout policy` (CLI 1.26.0, docker-default configuration).
  - Docker Scout counts 7 packages with copyleft licences (GPL, LGPL, MPL), all of them operating-system packages (it counts only packages whose licence it can read; the SBOM lists every component).
- Signed with ReadyStack's release key (fingerprint `04daa92344a52dbc`): https://readystack.dev/keys/cosign.pub.
- Runs as a non-root user (`portainer`).
- Attestations on the image: an SPDX SBOM and SLSA provenance v1.
- Rebuilt from this kit with network egress blocked on 2026-11-22; the rebuilt image digest is the published one.
- Base: Ubuntu 24.04.

The current grade, measured again every day, is on https://readystack.dev/products/portainer.

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

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/portainer/recipe. The complete kit is the release download. Each release is a tag here. How to report a vulnerability: [SECURITY.md](SECURITY.md).

## About ReadyStack

**Stable, Open-source Releases, Automated.** ReadyStack releases popular open-source apps every week with every available critical and high security fix applied, plus full documentation, reference data, tests and a build recipe that recreates each release bit-for-bit. Each release is rebuilt from its pinned inputs with the network off, checked against its published digest, signed, and scanned and graded again every day. The images and build kits are free, and ReadyStack is soon to be a nonprofit.

[readystack.dev](https://readystack.dev) · [All products](https://readystack.dev/products.html) · [Build kits on GitHub](https://github.com/readystack-dev) · [Defect log](https://readystack.dev/defects.html) · contact@readystack.dev

— ReadyStack · https://readystack.dev

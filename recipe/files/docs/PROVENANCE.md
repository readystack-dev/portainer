# Provenance — Portainer (`2.45.4-CE-ubuntu24.04-r1`)

Every item below is copied from a record in this archive; the record is named in brackets.

## Source

- Upstream repository: https://github.com/portainer/portainer
- Revision built: `2.45.4` (commit `505380c8eecff08cf513c457494bde91634db9ff`)
- Source tree: `b47db3d979f9f46e9c34be1ff42a9c1ba65a4502c5ecb137dd0869949e40acae` over 5417 files [`docs/provenance/SOURCE_TREE_HASH.json`]
- Community Edition only: enterprise code is removed or refused before the build (CE audit at acquire).

## Build

- Method: `source-rebuild-go`; base image `scratch + a chiselled Ubuntu 24.04 runtime (vendored/chisel/slices.txt, packages.tsv)`
- Compiled with `--network=none` from vendored source, dependencies and base images; BuildKit pinned to `moby/buildkit:v0.31.2` (shipped in `toolchain/`).
- SOURCE_DATE_EPOCH: `1795071769` [`SOURCE_DATE_EPOCH.txt`]
- Frozen inputs: [`docs/provenance/FREEZE_MANIFEST.json`], build recipe: [`docs/provenance/BUILD_RECIPE.json`].

## Output

- Published image: `readystack/portainer:2.45.4-CE-ubuntu24.04-r1` — index digest `sha256:2caa143ae419aa1a234c1cbf2ed65365061b8bef100a6b812ac664daae666b26` [`docs/provenance/LOCKED_DIGEST.txt`]
- linux/amd64 image digest `sha256:1812f46cdac0a4763b59fe067962c956b3ccf1ea0098939fc39c9ffdd9e809f1` — reproduced from this archive before publishing [`docs/provenance/REPRO_VERIFICATION.json`].

## Attestations and signature

- SBOM + SLSA provenance attached to the image: attached: an SPDX SBOM and SLSA v1 provenance [`docs/provenance/SCOUT_VERDICT.json`]
- cosign signature by the ReadyStack release key: verified before publishing. Check it: `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/portainer:2.45.4-CE-ubuntu24.04-r1`

## Pinned inputs, and why

- 41 pinned inputs, each with where it came from, why this one, how it was checked and when it was decided: `docs/PINS.md` [`docs/provenance/PINS.json`] (upstream source 2, base and build images 3, image digests 2, language runtimes and toolchains 1, dependency versions readystack sets 10, pins in the kit's dockerfiles 16, readystack's build engine 5, dependencies upstream chose 2).

## Build trail

- How this release passed through the ReadyStack harness, record by record (every chain, drive, stage, review round, defect and check, each naming the record it is copied from): `ReadyStack-portainer-2.45.4-CE-ubuntu24.04-r1.trail.json`, published beside this archive and signed with the release key (`ReadyStack-portainer-2.45.4-CE-ubuntu24.04-r1.trail.json.sigstore`), and readable at https://readystack.dev/products/portainer/trail/2.45.4-CE-ubuntu24.04-r1.


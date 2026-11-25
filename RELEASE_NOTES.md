# Portainer 2.45.4 — ReadyStack release `2.45.4-CE-ubuntu24.04-r1`

Generated 2026-11-22 from this release's build records and strategy. Statements that come from a single record name it in brackets; the others come from this release's strategy and build log.

## Release

- **Image:** `readystack/portainer:2.45.4-CE-ubuntu24.04-r1` (linux/amd64). Index digest `sha256:2caa143ae419aa1a234c1cbf2ed65365061b8bef100a6b812ac664daae666b26` [`docs/provenance/LOCKED_DIGEST.txt`].
- **Image manifest digest:** `sha256:1812f46cdac0a4763b59fe067962c956b3ccf1ea0098939fc39c9ffdd9e809f1` [`TARGET_DIGEST.txt`].
- **Upstream:** Portainer 2.45.4 built from source at `2.45.4` of https://github.com/portainer/portainer — upstream notes: https://github.com/portainer/portainer/releases/tag/2.45.4 [`docs/provenance/BUILD_RECIPE.json`].
- **Base image:** none (`FROM scratch`): a chiselled Ubuntu 24.04 runtime, the files Canonical's chisel cut from Ubuntu's own packages (`vendored/chisel/slices.txt`, `vendored/chisel/packages.tsv`); runtime user `portainer`.
- **Build:** `source-rebuild-go`, compiled offline with `--network=none`.
- **Supersedes:** ReadyStack release `2.45.3-CE-ubuntu24.04-r3`.

## What changed in this release

- Upstream version 2.45.3 → 2.45.4.
- Minimum dependency versions ReadyStack enforces on top of upstream (raised only where upstream's own version was lower); shipped versions from the SBOM [`docs/sbom/SBOM.json`]:
  - `golang.org/x/crypto` at least `v0.56.0`: not raised, upstream already pins `v0.57.0` (shipped: `v0.58.0`)
  - `golang.org/x/mod` at least `v0.40.0`: not raised, upstream already pins `v0.41.0` (shipped: `v0.41.0`)
  - `google.golang.org/grpc` at least `v1.83.2`: not raised, upstream already pins `v1.83.2` (shipped: `v1.83.2`)
  - `golang.org/x/net` raised from upstream's `v0.60.0` to at least `v0.62.0` (shipped: `v0.62.0`)
  - `github.com/moby/buildkit` raised from upstream's `v0.25.1` to at least `v0.28.1` (shipped: `v0.28.1`)
  - `github.com/containerd/containerd/v2` raised from upstream's `v2.2.5` to at least `v2.2.10` (shipped: `v2.2.10`)
  - `github.com/klauspost/compress` raised from upstream's `v1.18.7` to at least `v1.20.2` (shipped: `v1.20.2`)
- This release moves Portainer from 2.45.3 to 2.45.4, a newer release of upstream's 2.45.x line. Upstream's release notes list what changed: https://github.com/portainer/portainer/releases/tag/2.45.4

## Security status at release (measured 2026-11-22)

- **Docker Scout:** 0 fixable critical/high vulnerabilities; runs as `portainer` (non-root); SBOM + provenance attestations present (SPDX SBOM + SLSA v1) [`docs/provenance/SCOUT_VERDICT.json`].
- **OSV cross-check:** no fixable critical/high vulnerability beyond Docker Scout's findings.
- **Signature:** cosign signature verified by ReadyStack's release gate before publishing; check it yourself with `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/portainer:2.45.4-CE-ubuntu24.04-r1` (signatures are recorded in the public Sigstore transparency log).
- **ReadyStack release check at release:** passed (ReadyStack's own test, not a Docker Scout grade). Vulnerabilities are disclosed every day and the image never changes, so it is re-checked daily, beside Docker Scout's own dated grade, at https://readystack.dev/queue.
- **Before exposing this service:** Mounting /var/run/docker.sock gives Portainer, and anyone who logs in as its administrator, root-level control of the Docker host. Keep the UI on a trusted network and protect the administrator account.
- **Before exposing this service:** Port 9000 is plain HTTP. Prefer 9443 (HTTPS; a self-signed certificate is generated unless you pass --sslcert/--sslkey) and do not publish 9000 on untrusted networks.
- **Before exposing this service:** Creating the administrator account requires the setup token printed to the container log at each start while no administrator exists; do not start with --no-setup-token on a reachable network.

## Reproducibility

Rebuilds offline from this archive to the identical image digest `sha256:1812f46cdac0a4763b59fe067962c956b3ccf1ea0098939fc39c9ffdd9e809f1`: run `./BUILD_OFFLINE.sh`, then `./VERIFY_OFFLINE.sh` (add `--online` to confirm the Docker Hub tag holds the same digest). Before publishing, ReadyStack rebuilt the kit with `./BUILD_OFFLINE.sh` and compared the result with the published digest [`docs/provenance/REPRO_VERIFICATION.json`], then ran `./BUILD_OFFLINE.sh` and `./VERIFY_OFFLINE.sh` from this archive (without `--online`).

## Validation

- 3 of 3 use cases passed (3 authored) against the running image [`docs/validation/test-results.json`].
- The cases are `GET /` (200), `GET /api/status` (200), `GET /api/settings/public` (200); the suite checks nothing else.

## Known issues

- Open review finding about the release notes of `2.45.2-CE-ubuntu24.04-r2`, carried to this release because nothing shows it no longer applies: Claims a tested run of BUILD_OFFLINE.sh and VERIFY_OFFLINE.sh from the archive; the cited record shows only the rebuilt-digest comparison. [`RSD-portainer-9d1d65bf48`]

## Defects fixed

- 8 problems found before release and fixed before it shipped (8 by review); each is listed in `docs/defects/defects.json`.

## Verify this archive

```
sha256sum -c CHECKSUMS.sha256
./BUILD_OFFLINE.sh && ./VERIFY_OFFLINE.sh --online
cosign verify --key https://readystack.dev/keys/cosign.pub readystack/portainer:2.45.4-CE-ubuntu24.04-r1
```

ReadyStack records every signature in the public Sigstore transparency log (Rekor), so the command needs no extra flags.


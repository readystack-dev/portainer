# GENERATED L-009 hermetic build (--network=none, SBOM+SLSA-attestation-producing).
# Pinned bases from BASE_IMAGE_DIGESTS.lock; vendored Go tree + debs from Dockerfile.vendor.
FROM golang:1.26.11-bookworm@sha256:dc40a13b61304647ed7e5d581d246b86413dfc29d63c6d018310feb93cd98fc0 AS build_portainer
WORKDIR /src
COPY vendored/portainer-src/ .
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795071769
RUN go build -trimpath -ldflags='-s -w' -o /portainer ./api/cmd/portainer && /portainer --version && \
    { readelf -lW /portainer | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /portainer | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /portainer.needs
# rs-probe: the HEALTHCHECK helper (standard library only, from the kit's rs-probe.go)
FROM golang:1.26.11-bookworm@sha256:dc40a13b61304647ed7e5d581d246b86413dfc29d63c6d018310feb93cd98fc0 AS build_rs_probe
WORKDIR /probe
COPY rs-probe.go main.go
COPY rs-probe.mod go.mod
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOFLAGS="-buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795071769
RUN go build -trimpath -ldflags='-s -w' -o /rs-probe .
# the chiselled rootfs (vendored/chisel, cut by Dockerfile.vendor), the service user, the binaries
FROM ubuntu:24.04@sha256:9c7f200c07e3d4a03e7249d2c16bf66a51120fb876aa2242cf31451412543289 AS rootfs
ARG SOURCE_DATE_EPOCH=1795071769
ADD vendored/chisel/rootfs.tar /rootfs/
RUN printf 'portainer:x:999:999::/data:/bin/sh\n' >> /rootfs/etc/passwd && printf 'portainer:x:999:\n' >> /rootfs/etc/group && \
    mkdir -p /rootfs/data && chown -R 999:999 /rootfs/data
COPY --from=build_portainer /portainer /rootfs/usr/local/bin/portainer
COPY --from=build_portainer /portainer.needs /tmp/needs/portainer
COPY --from=build_rs_probe /rs-probe /rootfs/usr/local/bin/rs-probe
COPY --from=build_portainer /src/dist/public /rootfs/opt/portainer/public
COPY --from=build_portainer /src/mustache-templates /rootfs/opt/portainer/mustache-templates
RUN chmod 755 /rootfs/usr/local/bin/portainer /rootfs/usr/local/bin/rs-probe && \
    chown -R 999:999 /rootfs/opt/portainer/public && \
    chown -R 999:999 /rootfs/opt/portainer/mustache-templates
RUN --mount=type=bind,source=vendored/chisel,target=/chisel set -eu; \
    for n in /tmp/needs/*; do while read -r lib; do [ -n "$lib" ] || continue; \
      case "$lib" in /*) [ -e "/rootfs$lib" ] ;; *) [ -n "$(find /rootfs/usr/lib /rootfs/usr/lib64 -name "$lib" 2>/dev/null | head -1)" ] ;; esac || \
      { echo "$(basename "$n") needs $lib, which the chiselled rootfs does not have: add its slice to runtime_base.slices" >&2; exit 1; }; \
    done < "$n"; done; rm -rf /tmp/needs; \
    [ -e /rootfs/etc/os-release ] || { echo "no /etc/os-release: base-files_release-info is missing" >&2; exit 1; }; \
    [ "$(grep -c '^Package: ' /rootfs/var/lib/dpkg/status)" = "$(wc -l < /chisel/packages.tsv)" ] || \
      { echo "/var/lib/dpkg/status does not list every package of vendored/chisel/packages.tsv" >&2; exit 1; }; \
    rm -rf /rootfs/var/log/dpkg.log /rootfs/var/log/alternatives.log /rootfs/var/log/apt /rootfs/var/cache/ldconfig/aux-cache /rootfs/var/cache/fontconfig
FROM scratch
ARG SOURCE_DATE_EPOCH=1795071769
COPY --from=rootfs /rootfs/ /
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
LABEL org.opencontainers.image.title="Portainer"
LABEL org.opencontainers.image.version="2.45.4-CE-ubuntu24.04-r1"
LABEL org.opencontainers.image.licenses="Zlib"
LABEL org.opencontainers.image.source="https://github.com/portainer/portainer"
LABEL org.opencontainers.image.vendor="ReadyStack.dev"
LABEL org.opencontainers.image.description="Portainer Community Edition - container management GUI for Docker, Swarm and Kubernetes (single-container, embedded bbolt store)."
LABEL readystack.product="portainer"
LABEL readystack.edition="CE"
LABEL readystack.build_method="source-rebuild-go"
LABEL org.opencontainers.image.revision="505380c8eecff08cf513c457494bde91634db9ff"
HEALTHCHECK --interval=15s --timeout=5s --start-period=10s \
  CMD /usr/local/bin/rs-probe http://127.0.0.1:9000/api/status || exit 1
USER portainer
EXPOSE 9000 9443 8000
ENTRYPOINT ["portainer", "--data", "/data", "--assets", "/opt/portainer"]

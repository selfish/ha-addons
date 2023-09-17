ARG BUILD_FROM=ghcr.io/hassio-addons/debian-base/amd64:7.1.0
FROM $BUILD_FROM

# Set environment variables for integration and runtime
ENV DEBIAN_FRONTEND="noninteractive" \
    LANG="C.UTF-8" \
    TERM="xterm-256color" \
    PGID=0 \
    PUID=0 \
    WEBUI_PORT=8080

# Install rTorrent and clean up
RUN apt-get update && \
    apt-get install -y rtorrent && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Metadata as labels
LABEL maintainer="youcangetselfish@gmail.com" \
    org.opencontainers.image.title="rTorrent Addon for Home Assistant" \
    org.opencontainers.image.description="rTorrent BitTorrent client for Home Assistant" \
    org.opencontainers.image.licenses="MIT"

# Basic healthcheck for rTorrent process
HEALTHCHECK --interval=5s --retries=5 --start-period=30s --timeout=25s CMD pgrep rtorrent || exit 1

ENTRYPOINT ["rtorrent"]

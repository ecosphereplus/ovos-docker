ARG TAG=0.1.0
ARG REGISTRY=docker.io/aczire
FROM "${REGISTRY}/ovos-omva-base:${TAG}"

ARG BUILD_DATE=unknown
ARG VERSION=unknown
ARG TAG
ARG REGISTRY
ARG TAG
ARG REGISTRY

LABEL org.opencontainers.image.title="Open Voice OS OCI OMVA Voice ID plugin image"
LABEL org.opencontainers.image.description="Voice identification plugin using OMVA model for OVOS audio transformers"
LABEL org.opencontainers.image.version="${VERSION}"
LABEL org.opencontainers.image.created="${BUILD_DATE}"
LABEL org.opencontainers.image.documentation="https://openvoiceos.github.io/community-docs"
LABEL org.opencontainers.image.source="https://github.com/OpenVoiceOS/ovos-docker"
LABEL org.opencontainers.image.vendor="Open Voice OS"
LABEL org.opencontainers.image.licenses="Apache-2.0"
LABEL org.opencontainers.image.authors="Open Voice OS Community"
LABEL org.opencontainers.image.base.name="${REGISTRY}/ovos-omva-base:${TAG}"

ARG USER=ovos

USER root

SHELL ["/bin/bash", "-c"]

# Install only the OMVA Voice ID plugin (lightweight layer)
RUN source "/home/${USER}/.venv/bin/activate" \
  && pip install --no-cache-dir git+https://github.com/ecosphereplus/ovos-audio-transformer-plugin-omva-voiceid.git

USER "$USER"

ENTRYPOINT ["ovos-omva-voiceid-listener"]

WORKDIR "/home/${USER}"

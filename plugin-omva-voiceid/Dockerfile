ARG TAG=0.1.0
ARG REGISTRY=docker.io/smartgic
FROM "${REGISTRY}/ovos-sound-base:${TAG}"

ARG BUILD_DATE=unknown
ARG VERSION=unknown
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
LABEL org.opencontainers.image.base.name="${REGISTRY}/ovos-sound-base:${TAG}"

ARG USER=ovos

USER root

SHELL ["/bin/bash", "-c"]

# Install OMVA Voice ID plugin dependencies and plugin
RUN apt-get update \
  && apt-get install -o Dpkg::Options::="--force-confold" -y --no-install-recommends --no-install-suggests \
     build-essential python3-dev \
  && source "/home/${USER}/.venv/bin/activate" \
  && pip install git+https://github.com/ecosphereplus/ovos-audio-transformer-plugin-omva-voiceid.git \
  && apt-get --purge remove -y build-essential python3-dev \
  && apt-get --purge autoremove -y \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/* /var/log/{apt,dpkg.log} /tmp/* /var/tmp/* \
  && mkdir -p "/home/${USER}/.local/share/omva/models" \
  && chown "${USER}:${USER}" -R "/home/${USER}/.local/share/omva"

USER "$USER"

ENTRYPOINT ["ovos-omva-voiceid-listener"]

WORKDIR "/home/${USER}"

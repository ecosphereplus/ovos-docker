ARG TAG=0.1.0
ARG REGISTRY=docker.io/smartgic
FROM "${REGISTRY}/ovos-sound-base:${TAG}"

ARG BUILD_DATE=unknown
ARG VERSION=unknown
ARG TAG
ARG REGISTRY

LABEL org.opencontainers.image.title="OMVA Base Image with ML Dependencies"
LABEL org.opencontainers.image.description="Base image with OMVA Voice ID dependencies for OVOS audio transformers"
LABEL org.opencontainers.image.version="${VERSION}"
LABEL org.opencontainers.image.created="${BUILD_DATE}"
LABEL org.opencontainers.image.documentation="https://openvoiceos.github.io/community-docs"
LABEL org.opencontainers.image.source="https://github.com/ecosphereplus/ovos-docker"
LABEL org.opencontainers.image.vendor="Open Voice OS"
LABEL org.opencontainers.image.licenses="Apache-2.0"
LABEL org.opencontainers.image.authors="Open Voice OS Community"
LABEL org.opencontainers.image.base.name="${REGISTRY}/ovos-sound-base:${TAG}"

ARG USER=ovos

USER root

SHELL ["/bin/bash", "-c"]

# Install OMVA Voice ID plugin dependencies (major version pinning for stability)
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
     build-essential python3-dev \
  && source "/home/${USER}/.venv/bin/activate" \
  && pip install --no-cache-dir \
     "torch>=2.0,<3.0" \
     "torchaudio>=2.0,<3.0" \
     "speechbrain>=1.0,<2.0" \
     "transformers>=4.0,<5.0" \
     "librosa>=0.10,<1.0" \
     "soundfile>=0.12,<1.0" \
  && pip cache purge \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/archives/* /var/log/{apt,dpkg.log} /tmp/* /var/tmp/* \
           /home/${USER}/.cache/pip/* /root/.cache/pip/* \
  && mkdir -p "/home/${USER}/.local/share/omva/models" \
  && chown "${USER}:${USER}" -R "/home/${USER}/.local/share/omva"

USER "$USER"

WORKDIR "/home/${USER}"

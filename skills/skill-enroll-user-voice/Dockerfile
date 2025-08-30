ARG TAG=0.1.0
ARG REGISTRY=docker.io/smartgic
FROM "${REGISTRY}/ovos-skill-base:${TAG}"

ARG BUILD_DATE=unknown
ARG VERSION=unknown
ARG TAG
ARG REGISTRY

LABEL org.opencontainers.image.title="Open Voice OS OCI OMVA enroll-user-voice skill image"
LABEL org.opencontainers.image.description="OMVA skill for enrolling and managing user voice profiles for voice identification"
LABEL org.opencontainers.image.version="${VERSION}"
LABEL org.opencontainers.image.created="${BUILD_DATE}"
LABEL org.opencontainers.image.documentation="https://openvoiceos.github.io/community-docs"
LABEL org.opencontainers.image.source="https://github.com/OpenVoiceOS/ovos-docker"
LABEL org.opencontainers.image.vendor="Open Voice OS"
LABEL org.opencontainers.image.licenses="Apache-2.0"
LABEL org.opencontainers.image.authors="Open Voice OS Community"
LABEL org.opencontainers.image.base.name="${REGISTRY}/ovos-skill-base:${TAG}"

# Install dependencies and then clone and install the skill manually
RUN pip install ovos-workshop ovos-utils ovos-bus-client adapt-parser requests && \
    git clone https://github.com/ecosphereplus/ovos-skill-omva-enroll-voice.git /tmp/skill && \
    cd /tmp/skill && \
    mkdir -p omva_skill_voice_enrollment && \
    cp __init__.py constants.py version.py omva_skill_voice_enrollment/ && \
    cp -r locale omva_skill_voice_enrollment/ && \
    pip install . && \
    rm -rf /tmp/skill

ENTRYPOINT ["ovos-skill-launcher", "omva-skill-voice-enrollment.openvoiceos"]

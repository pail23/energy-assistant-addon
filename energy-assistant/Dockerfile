# https://developers.home-assistant.io/docs/add-ons/configuration#add-on-dockerfile
ARG BUILD_FROM
FROM $BUILD_FROM

# Execute during the build of the image
ARG TEMPIO_VERSION BUILD_ARCH EASS_VERSION

RUN \
    curl -sSLf -o /usr/bin/tempio \
    "https://github.com/home-assistant/tempio/releases/download/${TEMPIO_VERSION}/tempio_${BUILD_ARCH}"


RUN \
    apt-get update \
    && apt-get install -y --no-install-recommends \
        python3 \
        python3-pip \
    && pip install --break-system-packages energy-assistant==${EASS_VERSION}  \
    && mkdir /data \
    && rm -rf /var/lib/apt/lists/*
# Copy root filesystem
COPY rootfs /

VOLUME [ "/data" ]

EXPOSE 5000
ENV APP_CONFIG_FILE=local

LABEL \
    org.opencontainers.image.title="Energy Assistant" \
    org.opencontainers.image.description="Energy Assistant helps you to control your energy consumption." \
    org.opencontainers.image.source="https://github.com/pail23/energy-assistant-addon" \
    org.opencontainers.image.authors="The Energy Assistant Team" \
    org.opencontainers.image.documentation="https://github.com/pail23/energy-assistant-addon/discussions" \
    org.opencontainers.image.licenses="MIT" \
    io.hass.version=${EASS_VERSION} \
    io.hass.name="Energy Assistant" \
    io.hass.description="Energy Assistant Addon" \
    io.hass.platform="${TARGETPLATFORM}" \
    io.hass.type="addon"
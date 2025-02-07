FROM ghcr.io/geekswamp/android-sdk:latest

ARG FLUTTER_VERSION
ARG FLUTTER_CHANNEL

LABEL io.github.geekswamp.image.souce https://github.com/geekswamp/docker-flutter
LABEL io.github.geekswamp.image.version ${FLUTTER_VERSION}
LABEL org.opencontainers.image.source https://github.com/geekswamp/docker-flutter
LABEL org.opencontainers.image.description Flutter Docker image on Ubuntu Linux
LABEL org.opencontainers.image.licenses MIT

RUN useradd -ms /bin/bash flutter
ENV FLUTTER_DIR /home/flutter
ENV PATH "$PATH:$FLUTTER_DIR/flutter/bin"

RUN set -eux; apt-get update && apt-get upgrade -y \
    && apt-get install -y --no-install-recommends \
        clang \
        cmake \
        ninja-build \
        pkg-config \
        libgtk-3-dev \
    && apt-get autoremove -y \
    && apt-get autoclean -y

RUN git config --global --add safe.directory /home/flutter/flutter
RUN chown -R flutter:flutter ${FLUTTER_DIR}

USER flutter
WORKDIR ${FLUTTER_DIR}

RUN curl https://storage.googleapis.com/flutter_infra_release/releases/${FLUTTER_CHANNEL}/linux/flutter_linux_${FLUTTER_VERSION}.tar.xz -o flutter.tar.xz \
    && tar xf flutter.tar.xz \
    && rm flutter.tar.xz

RUN flutter config --no-analytics \
    && yes | flutter doctor --android-licenses \
    && flutter doctor -v

CMD ["flutter"]

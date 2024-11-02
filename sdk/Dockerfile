FROM ghcr.io/geekswamp/android-sdk:latest

ARG FLUTTER_VERSION
ARG FLUTTER_CHANNEL

LABEL io.github.geekswamp.image.souce https://github.com/geekswamp/docker-flutter
LABEL io.github.geekswamp.image.version ${FLUTTER_VERSION}
LABEL org.opencontainers.image.source https://github.com/geekswamp/docker-flutter
LABEL org.opencontainers.image.description Flutter Docker image on Ubuntu Linux
LABEL org.opencontainers.image.licenses MIT

ENV FLUTTER_DIR /home/root
ENV PATH "$PATH:$FLUTTER_DIR/flutter/bin"

WORKDIR ${FLUTTER_DIR}

RUN set -eux; apt-get update && apt-get upgrade -y \ 
  && apt-get install clang cmake ninja-build pkg-config libgtk-3-dev --no-install-recommends -y \
  && curl https://storage.googleapis.com/flutter_infra_release/releases/${FLUTTER_CHANNEL}/linux/flutter_linux_${FLUTTER_VERSION}.tar.xz -o flutter.tar.xz \
  && tar xf flutter.tar.xz \
  && rm flutter.tar.xz \
  && apt-get autoremove \
  && apt-get autoclean

RUN set -eux; yes | flutter doctor --android-licenses \
  && flutter config --no-analytics \
  && flutter doctor -v

CMD ["flutter"]
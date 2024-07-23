FROM ghcr.io/arifai/android-sdk:latest

ARG FLUTTER_VERSION
ARG FLUTTER_CHANNEL

LABEL io.github.arifai.image.souce https://github.com/arifai/docker-flutter
LABEL io.github.arifai.image.version ${FLUTTER_VERSION}
LABEL org.opencontainers.image.source https://github.com/arifai/docker-flutter
LABEL org.opencontainers.image.description Flutter Docker image on Ubuntu Linux
LABEL org.opencontainers.image.licenses MIT

ENV DOCKER_USER flutter
ENV FLUTTER_DIR /home/${DOCKER_USER}

RUN set -eux; mkdir -p ${FLUTTER_DIR}
ENV PATH "$PATH:$FLUTTER_DIR/flutter/bin"

RUN set -eux; groupadd -r ${DOCKER_USER} \
  && useradd -r -g ${DOCKER_USER} ${DOCKER_USER}

RUN set -eux; apt-get update && apt-get upgrade -y \ 
  && apt-get install clang cmake ninja-build pkg-config libgtk-3-dev -y --no-install-recommends \
  && curl https://storage.googleapis.com/flutter_infra_release/releases/${FLUTTER_CHANNEL}/linux/flutter_linux_${FLUTTER_VERSION}.tar.xz -o ${DOCKER_USER}.tar.xz \
  && mv ${DOCKER_USER}.tar.xz ${FLUTTER_DIR} \
  && cd ${FLUTTER_DIR} \
  && tar xf ${DOCKER_USER}.tar.xz \
  && rm ${DOCKER_USER}.tar.xz \
  && git config --global --add safe.directory ${FLUTTER_DIR}/${DOCKER_USER} \
  && chown -R ${DOCKER_USER}:${DOCKER_USER} ${FLUTTER_DIR}/${DOCKER_USER} \
  && apt-get autoremove \
  && apt-get autoclean

USER ${DOCKER_USER}

RUN set -eux; yes | flutter doctor --android-licenses \
  && flutter config --no-analytics \
  && flutter doctor -v

CMD ["flutter"]

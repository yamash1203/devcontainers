ARG ELIXIR_VERSION=latest
FROM elixir:${ELIXIR_VERSION}

ARG USERNAME=vscode
ARG USER_UID=1000
ARG NODE_VERSION=14
ARG PHOENIX_VERSION=1.5.7

RUN apt update \
    && curl -sL https://deb.nodesource.com/setup_${NODE_VERSION}.x | bash - \
    && apt install -y nodejs \
    && apt install -y inotify-tools \
    && apt install -y sudo \
    && useradd -s /bin/bash --uid ${USER_UID} -m ${USERNAME} \
    && echo "${USERNAME} ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/vscode \
    && chmod 0440 /etc/sudoers.d/vscode

USER ${USERNAME}
WORKDIR /home/${USERNAME}

RUN mix local.hex --force \
    && mix archive.install hex phx_new ${PHOENIX_VERSION} --force

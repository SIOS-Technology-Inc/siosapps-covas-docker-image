FROM node:16.14.0-buster

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367 && \
    apt update && \
    apt install -y \
    curl \
    bash \
    git \
    python3 \
    ansible \
    locales && \
    sed -i -E 's/# (ja_JP.UTF-8)/\1/' /etc/locale.gen && \
    locale-gen && \
    update-locale LANG=ja_JP.UTF8

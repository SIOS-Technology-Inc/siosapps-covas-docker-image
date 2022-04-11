FROM node:16.14.0-buster

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367 && \
    apt update && \
    apt install -y \
    curl \
    bash \
    git \
    python3 \
    ansible \
    language-pack-ja && \
    update-locale LANG=ja_JP.UTF8

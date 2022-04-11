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
    echo "ja_JP.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen ja_JP.UTF-8 && \
    update-locale LANG=ja_JP.UTF8
ENV LANG ja_JP.UTF-8
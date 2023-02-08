FROM node:16-buster
# Debian OS.

RUN echo "deb [check-valid-until=no] http://cdn-fastly.deb.debian.org/debian buster main" > /etc/apt/sources.list.d/buster.list && \
    sed -i '/deb http:\/\/deb.debian.org\/debian buster-updates main/d' /etc/apt/sources.list && \
    apt-get -o Acquire::Check-Valid-Until=false update && \
    apt-get -q install -y --no-install-recommends \
      ack-grep \
      bash \
      build-essential \
      cpio \
      cron \
      curl \
      git \
      g++ \
      htop \
      jq \
      parallel \
      rsync \
      supervisor \
      tree \
      wget \
      zip && \
    npm config set registry https://registry.npmjs.org/ && \
    echo "Install Spy filewatcher" && \
    cd /tmp && \
    wget -q https://github.com/jpillora/spy/releases/download/1.0.1/spy_linux_amd64.gz && \
    gunzip spy_linux_amd64.gz && \
    chmod 0755 spy_linux_amd64 && \
    mv spy_linux_amd64 /usr/bin/spy && \
    echo "Init supervisor" && \
    mkdir -p /etc/supervisor && \
    mkdir -p /var/log/supervisor && \
    echo "Increasing inotify watchers" && \
    touch /etc/sysctl.d/crashplan.conf && \
    echo "fs.inotify.max_user_watches=582222" > /etc/sysctl.d/crashplan.conf && \
    echo "Install dockerize" && \
    wget --quiet -O - https://github.com/jwilder/dockerize/releases/download/v0.6.1/dockerize-linux-amd64-v0.6.1.tar.gz | tar zxvf - && \
    mv dockerize /usr/bin
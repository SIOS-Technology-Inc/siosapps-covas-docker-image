FROM mongo:4.2

# mongo:4.2 (Ubuntu 18.04/bionic) 向けの MongoDB 社 apt リポジトリは
# 署名鍵が失効しており apt-get update がそのまま失敗するため、
# OSパッケージの更新中だけ一時的に無効化する。
RUN mv /etc/apt/sources.list.d/mongodb-org.list /etc/apt/sources.list.d/mongodb-org.list.disabled && \
    apt-get update && \
    apt-get upgrade -y && \
    mv /etc/apt/sources.list.d/mongodb-org.list.disabled /etc/apt/sources.list.d/mongodb-org.list && \
    rm -rf /var/lib/apt/lists/*

FROM ubuntu:22.04

RUN apt update && \
    apt install -y \
        curl
RUN curl -O https://autify-cli-assets.s3.us-west-2.amazonaws.com/autify-cli/channels/stable/autify-linux-x64.tar.gz && \
    tar -xzf ./autify-linux-x64.tar.gz && \
    ln -s /autify/bin/autify /usr/local/bin/autify && \
    autify --version
# トークンを作成してください
ENV AUTIFY_WEB_ACCESS_TOKEN=hoge
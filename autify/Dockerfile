FROM ubuntu:22.04

RUN apt-get update && \
    apt-get install -y curl
RUN curl https://autify-cli-assets.s3.amazonaws.com/autify-cli/channels/stable/install-standalone.sh | sh
# トークンを作成してください
ENV AUTIFY_WEB_ACCESS_TOKEN=hoge
FROM alpine:3.17

# Install OS dependencies.
RUN echo "System dependencies" && \
    apk update && \
    apk upgrade && \
    apk add --update \
      bash \
      curl \
      git \
      make \
      ca-certificates && \
    echo "MongoDB dependencies" && \
    apk add \
      mongodb-tools && \
    echo "Install migrate util" && \
    wget https://github.com/SIOS-Technology-Inc/covas-docker-image/releases/download/0.2.1/migrate && \
    chmod 0755 migrate && \
    mv migrate /usr/bin
FROM alpine:3.17

# Install OS dependencies.
RUN echo "System dependencies" && \
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
    wget https://github.com/SIOS-Technology-Inc/covas-docker-image/releases/download/v0.1.0/migrate && \
    chmod 0755 migrate && \
    mv migrate /usr/bin
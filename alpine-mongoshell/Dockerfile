FROM alpine:3.20

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
      mongodb-tools~=100.9.4 && \
    echo "Install migrate util" && \
    wget https://github.com/SIOS-Technology-Inc/siosapps-covas-migrate/releases/download/0.5.3/migrate-linux.zip && \
    unzip migrate-linux.zip && \
    chmod 0755 migrate && \
    mv migrate /usr/bin
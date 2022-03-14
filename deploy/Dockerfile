FROM alpine:3.9

ENV TF_VERSION 1.1.7

ENV ANSIBLE_VERSION 2.9.1
ENV AWSCLI_VERSION  1.16.293
ENV AZURE_VERSION   2.34.1
ENV DOCKER_COMPOSE  1.25.0
ENV DOCKER_ENGINE   4.1.0

RUN echo "System dependencies" && \
      apk add --update \
        bash \
        ca-certificates \
        curl \
        docker \
        git \
        gnupg \
        jq \
        make \
        nodejs \
        npm \
        openssl \
        python3 && \
    echo "Build dependencies" && \
      apk add --virtual build-deps \
        build-base \
        gcc \
        libffi-dev \
        musl-dev \
        openssl-dev \
        python3-dev && \
    echo "Python3 dependencies" && \
      python3 -m ensurepip && \
      pip3 install --upgrade pip cffi && \
      if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
      if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
    echo "Ansible dependencies" && \
      pip --no-cache-dir install \
        ansible==${ANSIBLE_VERSION} \
        docker-compose==${DOCKER_COMPOSE} \
        docker==${DOCKER_ENGINE} && \
    echo "Azure dependencies" && \
      pip --no-cache-dir install azure-cli==${AZURE_VERSION} && \
    echo "AWS dependencies" && \
      pip --no-cache-dir install awscli==${AWSCLI_VERSION} && \
    echo "Cleanup" && \
      apk del --purge build-deps && \
      rm -rf /var/cache/apk/*

RUN echo "Terraform dependencies" && \
      [[ "$(uname -m)" == "aarch64" ]] && export ARCH=arm64 || export ARCH=amd64 && \
      cd /tmp && \
      wget --quiet -O /tmp/terraform.zip https://releases.hashicorp.com/terraform/${TF_VERSION}/terraform_${TF_VERSION}_linux_${ARCH}.zip && \
      unzip /tmp/terraform.zip && \
      mv terraform /usr/bin && \
      rm -f /tmp/terraform.zip && \
    echo "Install migrate util" && \
      wget https://github.com/instoll/alpine-mongoshell/releases/download/0.1.0/migrate && \
      chmod 0755 migrate && \
      mv migrate /usr/bin && \
    echo "Sentry dependencies" && \
      npm config set unsafe-perm true && \
      npm install -g @sentry/cli

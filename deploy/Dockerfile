FROM alpine:3.15

ENV TF_VERSION 0.15.5
ENV TF_FILE    terraform_${TF_VERSION}_linux_amd64.zip

ENV ANSIBLE_VERSION 4.8.0
ENV AWSCLI_VERSION  1.22.54
ENV AZURE_VERSION   2.33.0
ENV DOCKER_COMPOSE  1.29.2
ENV DOCKER_ENGINE   5.0.3

# Install OS dependencies.
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
    echo "Terraform dependencies" && \
      cd /tmp && \
      wget https://releases.hashicorp.com/terraform/${TF_VERSION}/${TF_FILE} && \
      unzip ${TF_FILE} && \
      mv terraform /usr/bin && \
      rm -f ${TF_FILE} && \
    echo "Azure dependencies" && \
      pip --no-cache-dir install azure-cli==${AZURE_VERSION} && \
    echo "AWS dependencies" && \
      pip --no-cache-dir install awscli==${AWSCLI_VERSION} && \
    echo "Install migrate util" && \
      wget https://github.com/instoll/alpine-mongoshell/releases/download/0.1.0/migrate && \
      chmod 0755 migrate && \
      mv migrate /usr/bin && \
    echo "Sentry dependencies" && \
      npm config set unsafe-perm true && \
      npm install -g @sentry/cli && \
    echo "Cleanup" && \
      apk del --purge build-deps && \
      rm -rf /var/cache/apk/*

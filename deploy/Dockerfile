FROM ubuntu:22.04

ENV TF_VERSION 0.15.5
ENV TF_FILE    terraform_${TF_VERSION}_linux_amd64.zip

ENV ANSIBLE_VERSION 6.6.0
ENV AWSCLI_VERSION  1.22.54
ENV AZURE_VERSION   2.33.0
ENV DOCKER_COMPOSE  1.29.2
ENV DOCKER_ENGINE   5.0.3

# Install OS dependencies.
RUN echo "System dependencies" && \
      apt-get update && \
      apt-get install -y \
      gnupg \
      software-properties-common \
      curl \
      wget \
      ca-certificates \
      apt-transport-https \
      lsb-release \
      unzip \
      git \
      jq \
      make \
      python3-pip && \
    echo "dokcer dependencies" && \
      mkdir -m 0755 -p /etc/apt/keyrings && \
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg && \
      echo \
        "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
        $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null && \
      apt-get update && \
      apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin && \
    echo "nodejs dependencies" && \
      curl -fsSL https://deb.nodesource.com/setup_18.x | bash - && \
      apt-get install -y nodejs && \
    echo "Python3 dependencies" && \
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
      wget https://github.com/SIOS-Technology-Inc/covas-docker-image/releases/download/0.2.0/migrate && \
      chmod 0755 migrate && \
      mv migrate /usr/bin && \
    echo "Sentry dependencies" && \
      npm install -g @sentry/cli && \
    echo "Cleanup" && \
      apt-get clean

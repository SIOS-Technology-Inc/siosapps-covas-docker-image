# github actions でビルドするとめちゃくちゃ時間がかかるので手元の環境でビルドしてプッシュする
FROM ubuntu:24.04

ENV TF_VERSION=1.7.5
ENV TF_FILE=terraform_${TF_VERSION}_linux_amd64.zip
ENV ANSIBLE_VERSION=14.2.0
ENV AWSCLI_VERSION=2.25.12
ENV AZURE_VERSION=2.61.0

COPY ./azure-install.sh /azure-install.sh

# Install OS dependencies.
RUN echo "System dependencies" && \
  apt-get update && \
  apt-get upgrade -y && \
  apt-get install -y \
  gnupg \
  software-properties-common \
  curl \
  wget \
  ca-certificates \
  apt-transport-https \
  lsb-release \
  unzip \
  jq \
  make \
  python3-pip \
  python3-venv && \
  echo "git dependencies" && \
  add-apt-repository -y ppa:git-core/ppa && \
  apt-get update && \
  apt-get install -y git && \
  echo "dokcer dependencies" && \
  mkdir -m 0755 -p /etc/apt/keyrings && \
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg && \
  echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null && \
  apt-get update && \
  apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin && \
  echo "nodejs dependencies" && \
  curl -fsSL https://deb.nodesource.com/setup_22.x | bash - && \
  apt-get install -y nodejs && \
  npm install -g npm@latest && \
  npm install -g yarn && \
  echo "Python3 dependencies" && \
  if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
  if [ ! -e /usr/bin/python ]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
  python -m venv venv && \
  . venv/bin/activate && \
  pip install --upgrade pip cffi && \
  echo "Ansible dependencies" && \
  pip --no-cache-dir install \
  ansible==${ANSIBLE_VERSION} \
  requests && \
  echo "ログイン時にvenvを有効化する" && \
  echo "source /venv/bin/activate" >> /root/.bashrc && \
  echo "Terraform dependencies" && \
  cd /tmp && \
  wget https://releases.hashicorp.com/terraform/${TF_VERSION}/${TF_FILE} && \
  unzip ${TF_FILE} && \
  mv terraform /usr/bin && \
  rm -f ${TF_FILE} && \
  echo "Azure dependencies" && \
  # pip --no-cache-dir install azure-cli==${AZURE_VERSION} && \
  /azure-install.sh && \
  apt-get update && \
  apt-get install -y azure-cli=${AZURE_VERSION}-1~$(lsb_release -cs) && \
  echo "AWS dependencies" && \
  # pip --no-cache-dir install awscli==${AWSCLI_VERSION} && \
  curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64-${AWSCLI_VERSION}.zip" -o "awscliv2.zip" && \
  unzip awscliv2.zip && \
  aws/install && \
  rm -rf awscliv2.zip && \
  rm -rf aws && \
  echo "Install migrate util" && \
  wget https://github.com/SIOS-Technology-Inc/siosapps-covas-migrate/releases/download/0.7.0/migrate-linux.zip && \
  unzip migrate-linux.zip && \
  chmod 0755 migrate && \
  mv migrate /usr/bin && \
  echo "Sentry dependencies" && \
  npm install -g @sentry/cli && \
  echo "Cleanup" && \
  apt-get clean && apt-get autoremove -y

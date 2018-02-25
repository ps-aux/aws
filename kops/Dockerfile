FROM ubuntu:17.10
RUN apt update
RUN apt install --yes vim
RUN apt install --yes curl
RUN apt install --yes python-pip && \
    pip install awscli

# Kubectl & kops
ENV KUBECTL_VERSION=v1.9.3
ENV KOPS_VERSION=1.8.1

RUN curl -Lo kubectl "https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl" && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/local/bin/kubectl  && \
    curl -Lo kops  "https://github.com/kubernetes/kops/releases/download/${KOPS_VERSION}/kops-linux-amd64" > kops && \
    chmod +x ./kops  && \
    mv ./kops /usr/local/bin/


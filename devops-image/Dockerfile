ARG HELM_VERSION=3.11.2

FROM alpine/helm:${HELM_VERSION} as helm
# FROM debian:unstable-slim
FROM debian:12-slim

LABEL maintainer="Dmitry Nosulko <dnosulko@telematika.com>"

# kubectl is supported within one minor version (older or newer) of kube-apiserver. 1.18 will work with EKS 1.17
# https://kubernetes.io/docs/setup/release/version-skew-policy/
ARG KUBECTL_VERSION=v1.24.12
ADD requirements.txt /tmp/

RUN apt update \
  && apt upgrade -y \
  && apt install -y --no-install-recommends vim unzip git curl openssl openssh-client python3 python3-pip jq procps make age sshpass rsync kafkacat busybox \
  && pip3 install --no-cache-dir --break-system-packages -r /tmp/requirements.txt \
  && apt remove -y --purge python3-pip python-pip-whl python3-distutils python3-lib2to3 python3-pkg-resources python3-setuptools python3-wheel \
  && rm -rf /var/lib/apt/lists/* \
  && ln -s /usr/bin/busybox /usr/bin/ping \
  && echo "set mouse-=a" > /root/.vimrc

RUN echo "downloading kubectl ${KUBECTL_VERSION}" \
  && curl -L "https://dl.k8s.io/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl" -o /usr/local/bin/kubectl \
  && chmod +x /usr/local/bin/kubectl

COPY --from=helm /usr/bin/helm /usr/local/bin/helm

WORKDIR /opt

ENV TF_CLI_CONFIG_FILE=/terraform.rc

ENTRYPOINT [ "/bin/bash" ]

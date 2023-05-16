FROM ubuntu:jammy

ARG PYTHON_VERSION=3.9.5

RUN apt-get update -qq \
 && DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
      ca-certificates \
      curl \
      libev-dev \
      libuser \
      libuser1-dev \
 && rm -rf /var/lib/apt/lists/*

RUN curl -o rsp-session.tar.gz https://s3.amazonaws.com/rstudio-ide-build/session/jammy/amd64/rsp-session-jammy-2023.03.0-386.pro1-amd64.tar.gz \
 && mkdir -p /usr/lib/rstudio-server \
 && tar xzvf rsp-session.tar.gz -C /usr/lib/rstudio-server --strip-components=1 \
 && rm rsp-session.tar.gz

### Install Python version ###
RUN curl -O https://cdn.rstudio.com/python/ubuntu-2204/pkgs/python-${PYTHON_VERSION}_1_amd64.deb \
    && apt-get install -yq --no-install-recommends ./python-${PYTHON_VERSION}_1_amd64.deb \
    && rm -rf python-${PYTHON_VERSION}_1_amd64.deb \
    && /opt/python/${PYTHON_VERSION}/bin/python3 -m pip install --upgrade pip setuptools virtualenv

ENV PATH="/opt/python/${PYTHON_VERSION}/bin:${PATH}"
EXPOSE  8788/tcp

FROM ubuntu:jammy

ARG R_VERSION=4.3.0

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
 && rm rsp-session.tar.gz \
 && rm -rf /usr/lib/rstudio-server/bin/code-server/

### Install R version ###
RUN curl -O https://cdn.rstudio.com/r/ubuntu-2204/pkgs/r-${R_VERSION}_1_amd64.deb \
    && apt-get update -qq \
    && DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
         ./r-${R_VERSION}_1_amd64.deb \
	 libpq5 \
    && rm -f ./r-${R_VERSION}_1_amd64.deb \
    && rm -rf /var/lib/apt/lists/* \
    && ln -s /opt/R/${R_VERSION}/bin/R /usr/local/bin/R \
    && ln -s /opt/R/${R_VERSION}/bin/Rscript /usr/local/bin/Rscript


EXPOSE  8788/tcp

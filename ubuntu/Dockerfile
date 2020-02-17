FROM ubuntu:bionic

ARG P4_PORT=perforce:1666
ARG P4_HOST=workstation
ARG P4_USERNAME=root
ARG P4_PASSWORD=root
ARG P4_CLIENT=workspace

ENV TERM=xterm \
    P4PORT=${P4_PORT} \
    P4HOST=${P4_HOST} \
    P4USER=${P4_USERNAME} \
    P4PASSWD=${P4_PASSWORD} \
    P4CLIENT=${P4_CLIENT} \
    DEBIAN_FRONTEND=noninteractive \
    INITRD=No \
    LANG=en_US.utf8 \
    APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=DontWarn

RUN apt-get update \
    && apt-get install -y --no-install-recommends curl ca-certificates gnupg2  \
    && curl -fsSL https://package.perforce.com/perforce.pubkey | apt-key add - \
    && echo "deb http://package.perforce.com/apt/$(. /etc/os-release; echo "$ID")  $(. /etc/os-release; echo "$VERSION_CODENAME") release" > /etc/apt/sources.list.d/perforce.list \
    && apt-get update \
    && apt-get install helix-p4d -y --no-install-recommends \
    && mkdir -p /var/p4/project/ \
    && rm -rf /tmp/* /var/tmp/* \
              /var/lib/apt/lists/* \
              /var/cache/apt/archives/*.deb \
              /var/cache/apt/archives/partial/*.deb \
              /var/cache/apt/*.bin

WORKDIR /var/p4/project/

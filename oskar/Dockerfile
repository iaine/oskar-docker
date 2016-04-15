FROM ubuntu:14.04

RUN apt-get install -y software-properties-common

RUN add-apt-repository ppa:radio-astro/main && \
add-apt-repository multiverse

RUN apt-get update && \
    apt-get install -y oskar=2.6.1-1trusty && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

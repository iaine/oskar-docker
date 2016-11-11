FROM ubuntu:16.04

RUN apt-get update

RUN apt-get install -y software-properties-common

RUN add-apt-repository -s ppa:kernsuite/kern-1 && \
add-apt-repository multiverse

RUN apt-get update && \
    apt-get install -y oskar && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

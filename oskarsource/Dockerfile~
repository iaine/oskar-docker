FROM ubuntu:14.04

# build from source

# taken from NVIDIA Docker file
# https://github.com/NVIDIA/nvidia-docker/blob/master/ubuntu-14.04/cuda/7.5/runtime/Dockerfile

ENV NVIDIA_GPGKEY_SUM bd841d59a27a406e513db7d405550894188a4c1cd96bf8aa4f82f1b39e0b5c1c
ENV NVIDIA_GPGKEY_FPR 889bee522da690103c4b085ed88c3d385c37d3be

RUN apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/GPGKEY && \
    apt-key adv --export --no-emit-version -a $NVIDIA_GPGKEY_FPR | tail -n +2 > cudasign.pub && \
    echo "$NVIDIA_GPGKEY_SUM  cudasign.pub" | sha256sum -c --strict - && rm cudasign.pub && \
    echo "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1404/x86_64 /" > /etc/apt/sources.list.d/cuda.list

ENV CUDA_VERSION 7.5
LABEL com.nvidia.cuda.version="7.5"

ENV CUDA_PKG_VERSION 7-5=7.5-18
RUN apt-get update && apt-get install -y --no-install-recommends --force-yes \
        cuda && \
    ln -s cuda-$CUDA_VERSION /usr/local/cuda

RUN echo "/usr/local/cuda/lib" >> /etc/ld.so.conf.d/cuda.conf && \
    echo "/usr/local/cuda/lib64" >> /etc/ld.so.conf.d/cuda.conf && \
    ldconfig

RUN echo "/usr/local/nvidia/lib" >> /etc/ld.so.conf.d/nvidia.conf && \
    echo "/usr/local/nvidia/lib64" >> /etc/ld.so.conf.d/nvidia.conf

ENV PATH /usr/local/nvidia/bin:/usr/local/cuda/bin:${PATH}
ENV LD_LIBRARY_PATH /usr/local/nvidia/lib:/usr/local/nvidia/lib64:${LD_LIBRARY_PATH}

RUN apt-get install -y software-properties-common && \
add-apt-repository ppa:radio-astro/main && \
add-apt-repository multiverse && \
apt-get update && \
apt-get install -y casacore2=2.0.3-2trusty \
cmake \
g++ \
liblapack-dev \
libqt4-dev \
unzip \
wget

# now build OSKAR
RUN wget http://oskar.oerc.ox.ac.uk/old-site/OSKAR-Source.zip && \
unzip OSKAR-Source.zip && \
mkdir -p OSKAR-2.6.1-Source/build && \
cd OSKAR-2.6.1-Source/build && \
cmake ../ && \
make && \
make install

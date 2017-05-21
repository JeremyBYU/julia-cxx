FROM ubuntu:14.04

LABEL maintainer "jeremybyu@gmail.com"

ARG DEBIAN_FRONTEND=noninteractive

ENV JULIA_DOWNLOAD_URL https://julialang.s3.amazonaws.com/bin/linux/x64/0.5/julia-0.5.2-linux-x86_64.tar.gz
ENV PATH /julia/usr/bin:$PATH
ENV CXX_VERSION fe0827de1cc63ba6deb352bb292d3b2394b11c60

RUN apt-get update && \
    apt-get install -y software-properties-common python-software-properties && \
    add-apt-repository -y ppa:ubuntu-toolchain-r/test && \
    apt-get update && \
    apt-get install -y \
    man-db \
    less \
    git \
    perl \
    m4 \
    unzip \
    bzip2 \
    cmake \
    wget \
    curl \
    pkg-config \
    build-essential \
    gcc-6 \
    g++-6 \
    gfortran \
    libblas-dev \
    liblapack-dev \
    libgmp-dev \
    libmpfr-dev \
    libssl-dev \
    libc6 \
    libc6-dev \
    libedit-dev \
    libncurses5-dev \
    python \
    python-dev && \
    apt-get clean

RUN mkdir -p /julia/usr && \
    wget -O /julia/julia.tar.gz $JULIA_DOWNLOAD_URL && \
    tar -xvzf /julia/julia.tar.gz -C /julia/usr/ --strip-components 1 && \
    rm /julia/julia.tar.gz


RUN /julia/usr/bin/julia -e 'Pkg.clone("https://github.com/r9y9/Cxx.jl")' && \
    cd `/julia/usr/bin/julia -e 'print(Pkg.dir("Cxx"))'` && \
    git checkout $CXX_VERSION && \
    /julia/usr/bin/julia -e 'Pkg.build("Cxx")'

FROM ubuntu:16.04
MAINTAINER robin@kingsquare.nl

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        flex \
        bison \
        gcc \
        pkg-config \
        cmake \
        build-essential \
        libedit-dev \
        libfcgi-dev \
        libbz2-dev \
        libpcre3-dev \
        libicu-dev \
        libcunit1-dev \
        libxml2-dev \
        git \
        python \
        libtool \
        autoconf \
        automake \
        ca-certificates

RUN git clone --depth=1 https://github.com/saffire/saffire.git /opt/saffire && \
    cd /opt/saffire && \
    git submodule init && \
    git submodule update && \
    sh build.sh

RUN mkdir -p /var/app
WORKDIR /var/app
COPY raffler.sf /var/app

# create the symlink for the actual file
RUN ln -s /var/names/current /var/app/users.txt

CMD ["/opt/saffire/build/release/bin/saffire", "/var/app/raffler.sf", "/var/names/current"]

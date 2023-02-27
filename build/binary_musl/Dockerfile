FROM golang:1.18
LABEL maintainer="Mingxia Cai"

# # The image is used to build chaosblade for musl
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak && \
    sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list && \
    sed -i 's/security.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list && \
    wget http://www.musl-libc.org/releases/musl-1.1.21.tar.gz \
    && tar -zxvf musl-1.1.21.tar.gz \
    && rm musl-1.1.21.tar.gz \
    && cd musl* \
    && ./configure \
    && make \
    && make install \
    && rm -rf musl*

RUN apt-get update \
    && apt-get install unzip

ENV CC /usr/local/musl/bin/musl-gcc
ENV GOOS linux

ENTRYPOINT [ "make" ]
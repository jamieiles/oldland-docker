FROM ubuntu:vivid
MAINTAINER Jamie Iles <jamie@jamieiles.com>
RUN apt-get update
RUN apt-get install -y build-essential git texinfo flex bison libgmp-dev file libmpfr-dev libmpc-dev zlib1g-dev libc6-dev-i386

RUN mkdir -p /build/BUILD
WORKDIR /build
ADD binutils-gdb-oldland/ binutils-gdb-oldland
ADD gcc-oldland gcc-oldland/
ADD newlib-oldland newlib-oldland/

RUN mkdir /build/BUILD/binutils
RUN mkdir /build/BUILD/gcc
RUN mkdir /build/BUILD/newlib

WORKDIR /build/BUILD/binutils
RUN ../../binutils-gdb-oldland/configure --target=oldland-elf
RUN make
RUN make install

WORKDIR /build/BUILD/gcc
RUN ../../gcc-oldland/configure --target=oldland-elf --disable-libquadmath --disable-libssp --enable-languages=c --disable-shared --with-headers --enable-multilib --with-newlib
RUN make all-gcc
RUN make install-gcc

WORKDIR /build/BUILD/newlib
RUN ../../newlib-oldland/configure --target=oldland-elf --with-newlib
RUN make
RUN make install

WORKDIR /build/BUILD/gcc
RUN make
RUN make install

WORKDIR /
RUN rm /build -rf

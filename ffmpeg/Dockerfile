#Detail:https://trac.ffmpeg.org/wiki/CompilationGuide/Ubuntu
FROM ubuntu:22.04

#These are packages required for compiling, but you can remove them when you are done if you prefer:
RUN sudo apt-get update -qq && sudo apt-get -y install \
    autoconf \
    automake \
    build-essential \
    cmake \
    git-core \
    libass-dev \
    libfreetype6-dev \
    libgnutls28-dev \
    libmp3lame-dev \
    libsdl2-dev \
    libtool \
    libva-dev \
    libvdpau-dev \
    libvorbis-dev \
    libxcb1-dev \
    libxcb-shm0-dev \
    libxcb-xfixes0-dev \
    meson \
    ninja-build \
    pkg-config \
    texinfo \
    wget \
    yasm \
    zlib1g-dev

RUN apt-get install nasm

#On Ubuntu 20.04 you may also need this command: (​note)
RUN apt install libunistring-dev libaom-dev libdav1d-dev

RUN apt-get clean 

FROM ubuntu:22.04

RUN apt-get update
RUN apt-get install -y sudo
RUN apt-get install -y \
        build-essential clang flex bison g++ gawk gcc-multilib g++-multilib \
gettext git libncurses-dev libssl-dev python3-distutils rsync unzip zlib1g-dev \
file wget
RUN apt-get clean
RUN useradd -m user
RUN echo 'user ALL=NOPASSWD: ALL' > /etc/sudoers.d/user

# set system wide dummy git config
RUN git config --system user.name "user"
RUN git config --system user.email "user@example.com"

USER user
WORKDIR /home/user

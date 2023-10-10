#https://openwrt.org/docs/guide-developer/toolchain/install-buildsystem
FROM alpine

#useradd not found
RUN apk add shadow
#/etc/sudoers.d not exist
RUN apk add sudo
#
RUN apk add argp-standalone asciidoc bash bc binutils bzip2 cdrkit coreutils \
  diffutils elfutils-dev findutils flex musl-fts-dev g++ gawk gcc gettext git \
  grep gzip intltool libxslt linux-headers make musl-libintl musl-obstack-dev \
  ncurses-dev openssl-dev patch perl python3-dev rsync tar \
  unzip util-linux wget zlib-dev
 
# python2-dev required for OpenWrt 19.07 and earlier is not available on Alpine Linux 3.16 and newer 
 
# missing dependency workaround (libtinfo is not installable by any APK package,
# but can be simulated via libncurses (see: https://stackoverflow.com/a/41517423 )
# w/o this - ERROR: package/boot/uboot-mvebu failed to build (build variant: clearfog)
RUN ln -s /usr/lib/libncurses.so /usr/lib/libtinfo.so

RUN useradd -m user
RUN echo 'user ALL=NOPASSWD: ALL' > /etc/sudoers.d/user

# set system wide dummy git config
RUN git config --system user.name "user"
RUN git config --system user.email "user@example.com"

USER user
WORKDIR /home/user

FROM ubuntu:18.04

#传入参数
ARG userid
ARG groupid
ARG username

# 解决 debconf: unable to initialzie frontend: Dialog
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get clean
RUN apt-get update

#https源可能会报证书相关错误
#RUN apt-get install -y ca-certificates
RUN apt-get install -y curl

#arm host 会报 404 NOT FOUND，华为源包含arm相关依赖，但是无法安装i386相关依赖
#RUN curl -o /etc/apt/sources.list https://repo.huaweicloud.com/repository/conf/Ubuntu-Ports-bionic.list

#获取中科大源
RUN curl -o /etc/apt/sources.list https://mirrors.ustc.edu.cn/repogen/conf/ubuntu-http-4-bionic
RUN apt-get update

#安装编译所需依赖
RUN apt-get install -y git-core gnupg flex bison build-essential zip curl zlib1g-dev libc6-dev-i386 libncurses5 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig

#安装python3并命名
RUN apt-get install -y python3
#RUN update-alternatives --remove-all python & 2 > /dev/null
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 100
RUN update-alternatives --config python 

#源码编译过程中找不到rsync命令
RUN apt-get install -y rsync

RUN apt-get autoremove -y

# 最新的AOSP源码中已经带了JDK，所以无需安装
# RUN curl -o jdk8.tgz https://android.googlesource.com/platform/prebuilts/jdk/jdk8/+archive/master.tar.gz \
#  && tar -zxf jdk8.tgz linux-x86 \
#  && mv linux-x86 /usr/lib/jvm/java-8-openjdk-amd64 \
#  && rm -rf jdk8.tgz

#下载repo
RUN curl -o /usr/local/bin/repo https://storage.googleapis.com/git-repo-downloads/repo && chmod a+x /usr/local/bin/repo

#添加用户、组、.gitcofig
RUN groupadd -f -g $groupid $username || true \
 && useradd -m -u $userid -g $groupid $username \
 && echo $username >/root/username \
 && echo "export USER="$username >>/home/$username/.gitconfig
COPY gitconfig /home/$username/.gitconfig
RUN chown $userid:$groupid /home/$username/.gitconfig
ENV HOME=/home/$username
ENV USER=$username

ENTRYPOINT chroot --userspec=$(cat /root/username):$(cat /root/username) / /bin/bash -i


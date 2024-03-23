FROM ubuntu:20.04

#传入参数
ARG userid
ARG groupid
ARG username

# 解决 debconf: unable to initialzie frontend: Dialog
ENV DEBIAN_FRONTEND noninteractive

RUN sed -i 's#archive.ubuntu.com#mirrors.tuna.tsinghua.edu.cn/ubuntu#g' /etc/apt/sources.list
RUN sed -i 's#security.ubuntu.com#mirrors.tuna.tsinghua.edu.cn/ubuntu#g' /etc/apt/sources.list

#设置语言
RUN apt-get update 
RUN apt-get install -y locales && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8

#安装必须的依赖
RUN apt-get install -y ca-certificates
RUN apt install -y curl wget vim sudo
#安装编译所需依赖
RUN apt-get install -y git-core gnupg flex bison build-essential zip curl zlib1g-dev libc6-dev-i386 libncurses5 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig

#安装python3并命名
RUN apt-get install -y python3
#RUN update-alternatives --remove-all python > /dev/null
RUN update-alternatives --install /usr/bin/python python /usr/bin/python3 100
#清除缓存文件
RUN apt-get autoremove

#下载repo
RUN curl -o /usr/local/bin/repo https://storage.googleapis.com/git-repo-downloads/repo && chmod a+x /usr/local/bin/repo

#新建用户
RUN groupadd -f -g $groupid $username || true \
 && useradd -m -u $userid -g $groupid $username \
 && echo $username >/root/username \
 && echo "export USER="$username >>/home/$username/.gitconfig
COPY gitconfig /home/$username/.gitconfig
RUN chown $userid:$groupid /home/$username/.gitconfig
ENV HOME=/home/$username
ENV USER=$username

#设置root密码
RUN echo 'root:root' | chpasswd
RUN echo "$username ALL=(ALL) NOPASSWD: ALL">>/etc/sudoers

ENTRYPOINT chroot --userspec=$(cat /root/username):$(cat /root/username) / /bin/bash -i


### 当前已归档的编译环境

* AOSP
* Openwrt

### 使用Docker遇到的一些坑

host为Manjaro Linux，安装官方源里的`docker`包,此时如果同时安装`docker-desktop`包则会出现文件挂载权限混乱问题。

需要注意的是，使用docker最好以非`root`用户编译镜像以及运行容器。

参考官方文档进行操作：https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user

首先创建`docker`组：
```shell
sudo groupadd docker

```
然后将当前用户加入到`docker`组：
```shell
sudo usermod -aG docker $(id -un)
```
重新登陆或者重启系统组成员就会生效了。
或者通过运行命令来达到同样的目的:
```shell

newgrp docker
```
使用以下命令测试普通用户是否可以运行`docker`：
```shell

docker version
```
注意：如果提示与`~/.docker/*`有关的错误，请`rm -rf ~/.docker`后重试。

使用如下命令设置`docker`守护进程开机启动：
```shell
sudo systemctl enable docker.service
```

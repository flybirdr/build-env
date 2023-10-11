* 官方链接
https://openwrt.org/docs/guide-developer/toolchain/install-buildsystem

* 需要注意的是开发或者编译过程中不应切换编译环境，比如从`alpine`切换到`ubuntu`由于环境软件版本差异，编译工具链会用到环境内的工具比如`python3`，切换环境会导致编译工具链文件链接失效导致编译失败。本人遇到过从`alpine`切换到`ubuntu`导致`staging_dir/host/bin/python*`链接失效导致编译失败。
* 切换编译环境需要执行`make dirclean`

## 注意事项

* 官方链接
https://openwrt.org/docs/guide-developer/toolchain/install-buildsystem

* 编译过程参考：https://p3terx.com/archives/openwrt-compilation-steps-and-commands.html

* 需要注意的是开发或者编译过程中不应切换编译环境，比如从`alpine`切换到`ubuntu`由于环境软件版本差异，编译工具链会用到环境内的工具比如`python3`，切换环境会导致编译工具链文件链接失效导致编译失败。本人遇到过从`alpine`切换到`ubuntu`导致`staging_dir/host/bin/python*`链接失效导致编译失败。

* 切换编译环境需要执行`make dirclean`

* 编译失败请运行`make -j1 V=s`查看具体错误信息

* 如果是使用CI执行编译任务则可以编译命令则可以写成`make -j$(nproc) || make -j1 || make -j1 V=s`方便查看错误信息。

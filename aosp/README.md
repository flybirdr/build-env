The Dockerfile in this directory sets up an Ubuntu Trusty image ready to build
a variety of Android branches (>= Lollipop). It's particulary useful to build
older branches that required 14.04 if you've upgraded to something newer.

First, build the image:
```
# Copy your host gitconfig, or create a stripped down version
$ cp ~/.gitconfig gitconfig
$ docker build --build-arg userid=$(id -u) --build-arg groupid=$(id -g) --build-arg username=$(id -un) -t android-build-trusty .
```

Then you can start up new instances with:
```
$ docker run -it --rm -v $(pwd):/src android-build-trusty
> cd /src; source build/envsetup.sh
> lunch aosp_arm-eng
> m -j50
```

在MacOs上使用
确保Docker已开启`Use Rosetta for x86_64/amd64 emulation on Apple Silicon`选项
`docker build`命令增加`--platform linux/amd64`选项
`docker run`命令增加`--platform linux/amd64`选项

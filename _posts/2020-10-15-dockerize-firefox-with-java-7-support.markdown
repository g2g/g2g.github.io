---
title: Dockerize Firefox with Java 7 support
date: 2020-10-15T23:58:08+01:00
---
... for old Raritan PDU/KVM devices Web access

## Build your Docker image from Dockerfile ##

* create your Dockerfile

#### **`Dockerfile`**
```bash
FROM i386/debian:jessie

RUN apt-get update && apt-get install -y firefox-esr icedtea-plugin icedtea-netx openjdk-7-jre openjdk-7-jre-headless tzdata-java
RUN useradd -ms /bin/bash firefox
ENV MOZ_FORCE_DISABLE_E10S=1
USER firefox
WORKDIR /home/firefox
```

* build it
```bash
docker build -t firefox .                 # make it great again
docker images --filter reference=firefox  # check your docker image information
```

## Run your Docker container ##

```bash
docker run -it --rm -e DISPLAY=${DISPLAY} -v /tmp/.X11-unix:/tmp/.X11-unix -v $HOME/Downloads:/home/firefox/Downloads firefox firefox                                        # run it with sharing Downloads directory
alias ffjava7='docker run -it --rm -e DISPLAY=${DISPLAY} -v /tmp/.X11-unix:/tmp/.X11-unix -v $HOME/Downloads:/home/firefox/Downloads firefox firefox' | tee -a $HOME/.bashrc # add an alias to make access simplier
```

## Sources ##

* how to build your Docker container
  * <https://blog.yadutaf.fr/2017/09/10/running-a-graphical-app-in-a-docker-container-on-a-remote-server/>
  * <https://www.sicpers.info/2020/10/running-linux-gui-apps-under-macos-using-docker/> [Mac OSX]
* fix Firefox tab persistently crashes on some sites
  * <https://support.mozilla.org/bm/questions/1266719>


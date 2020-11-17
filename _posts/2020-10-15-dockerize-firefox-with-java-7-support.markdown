---
title: Dockerize persistent Firefox with Java 7 support
date: 2020-10-15T23:58:08+01:00
---
... for old Raritan PDU/KVM devices Web access

## Build your Docker image from Dockerfile ##

* create your Dockerfile
#### **`Dockerfile`**
```dockerfile
FROM i386/debian:jessie
RUN apt-get update && apt-get install -y firefox-esr icedtea-plugin icedtea-netx openjdk-7-jre openjdk-7-jre-headless tzdata-java
RUN useradd -ms /bin/bash firefox
ENV MOZ_FORCE_DISABLE_E10S=1
USER firefox
WORKDIR /home/firefox
CMD tail -f /dev/null
```
`tail -f /dev/null` force your Docker container to be **persistent** even if you've closed your Firefox session

* build it
```bash
docker build -t firefox .                 # make it great again
docker images --filter reference=firefox  # check your docker image information
```

## Run your Docker container ##

* pop Firefox
```bash
docker run -it --rm -e DISPLAY=${DISPLAY} -v /tmp/.X11-unix:/tmp/.X11-unix -v $HOME/Downloads:/home/firefox/Downloads firefox firefox                                        # run it with sharing Downloads directory
```

* add it to your .bashrc to simplify Firefox docker access
#### **`.bashrc`**
```bash
function ffjava7(){
  CONTAINER_NAME=firefox
  xhost +;
  docker container inspect ${CONTAINER_NAME} > /dev/null 2>&1 ; [ $? -eq 0  ] \
    && docker start firefox \
    || docker run -d --name ${CONTAINER_NAME} -e DISPLAY=${DISPLAY} -v /tmp/.X11-unix:/tmp/.X11-unix -v $HOME/Downloads:/home/firefox/Downloads firefox firefox
}
```

## Sources ##

* how to build your Docker container
  * <https://blog.yadutaf.fr/2017/09/10/running-a-graphical-app-in-a-docker-container-on-a-remote-server/>
  * <https://www.sicpers.info/2020/10/running-linux-gui-apps-under-macos-using-docker/> [Mac OSX]
  * <https://github.com/jlesage/docker-firefox>
  * <https://github.com/findepi/docker.firefox-silverlight-pipelight> [Silverlight support]
* fix Firefox tab persistently crashes on some sites
  * <https://support.mozilla.org/bm/questions/1266719>


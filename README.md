[![Build Status](https://gitlab.com/canyan/janus-gateway-docker/badges/master/pipeline.svg)](https://gitlab.com/canyan/janus-gateway-docker/pipelines) [![Docker pulls](https://img.shields.io/docker/pulls/canyan/janus-gateway.svg?maxAge=3600)](https://hub.docker.com/repository/docker/canyan/janus-gateway)

# Janus WebRTC Server

This repository provides the Dockerfile to build a full-featured docker image for the [Janus WebRTC Server](https://github.com/meetecho/janus-gateway) based on Debian buster.

Janus is an open source, general purpose, WebRTC server designed and developed by [Meetecho](http://www.meetecho.com). This version of the server is tailored for Linux systems, although it can be compiled for, and installed on, MacOS machines as well. Windows is not supported, but if that's a requirement, Janus is known to work in the "Windows Subsystem for Linux" on Windows 10.

For some online demos and documentations, make sure you pay the [project website](https://janus.conf.meetecho.com/) a visit!

To discuss Janus with us and other users, there's a Google Group called [meetecho-janus](https://groups.google.com/forum/#!forum/meetecho-janus) that you can use. If you encounter bugs, though, please submit an issue on [github](https://github.com/meetecho/janus-gateway/issues) instead.

## Usage

You can use the docker image as follows:

```bash
$ docker pull canyan/janus-gateway:latest
```

We provide the following tags:

* **latest**: points to the latest stable version
* **full version number (e.g., 0.10.7)**
* **major version number (e.g., 0.10)**
* **master**: daily rebuild of the master branch

You can use the docker-image in a docker-compose project including:

```yaml
version: '2.1'
services:

  #
  # janus-gateway
  #
  janus-gateway:
    image: 'canyan/janus-gateway:0.10.7'
    command: ["/usr/local/bin/janus", "-F", "/usr/local/etc/janus"]
    ports:
      - "8188:8188"
      - "8088:8088"
      - "8089:8089"
      - "8889:8889"
      - "8000:8000"
      - "7088:7088"
      - "7089:7089"
    volumes:
      - "./etc/janus/janus.jcfg:/usr/local/etc/janus/janus.jcfg"
      - "./etc/janus/janus.eventhandler.sampleevh.jcfg:/usr/local/etc/janus/janus.eventhandler.sampleevh.jcfg"
    restart: always
```

## Authors

This is a Here.fm fork of the dockerfile originally maintained by Canyan.io

Build this and save it:

sudo docker save -o ./herefm-janus-docker.tar herefm/janus-gateway:multistream

## Building

git clone git@github.com:meetecho/janus-gateway.git

Check out whichever branch you want to build
cp Dockerfile from this repo into the janus-gateway directory
sudo docker build -t herefm/janus-gateway:multistream .


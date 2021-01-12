---
layout: post
title: Learning Docker
published: true
---

## Docker setup in Mac
* Install docker in mac

*맥에 도커 설치 하기*

    1. Download Docker Desktop for Mac from https://hub.docker.com/editions/community/docker-ce-desktop-mac

    *도커 홈페이지에서 도커 데스크탑 다운로드*

    2. Double click icon and drag into Application

    *더블클릭으로 설치*

* Docker version check

*도커 버전 확인*
```bash
$ docker version
```

* Docker ubuntu 20.04 LTS image install

*도커에 우분투 20.04 이미지 인스톨*
```bash
$ docker run  -d -t --name ubuntu ubuntu:20.04
```

* Run contatiner (want exit? —> $ exit)

*컨테이너 시작*
```bash
$ docker exec -it ubuntu bash
```

* Version check

*컨테이너 버전 확인*
```bash
$ cat /etc/os-release
```

* Check running container

*실행중인 컨테이너 확인*
```bash
$ docker ps
```

* Stop container

*컨테이너 스톱*
```bash
$ docker stop [container_id]
```

* Check stopped container / checking deleted container

*멈췄거나 삭제된 컨테이너 확인*
```bash
$ docker ps -a
```

* Delete container

*컨테이너 삭제*
```bash
$ docker rm [container_id1] [container_id2]
```

* Currently installed images check

*현재 설치된 이미지 확인*
```bash
$ docker images
```

* Delete image

*이미지 삭제*
```bash
$ docker rmi [img_id]
```

* Delete container b4 deleting image

*컨테이너 지우고 이미지 삭제*
```bash
$ docker rmi -f [img_id]
```

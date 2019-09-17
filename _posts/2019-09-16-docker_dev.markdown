---
layout: post
title:  "docker을 이용한 개발환경 셋팅 CI + MYSQL (for windows7)"
date:   2019-09-16 10:00
author: jizero
tags:	['docker','codeigniter']
img:  201909/php1.png # Add image post (optional)
---

## 목표
로컬환경에 개발환경을 설치하지 않고 docker를 이용해 개발환경을 구성해보자!

ubuntu 16<br /> 
php 7.3<br />
codeigniter 3.10.<br />
mysql 5.7<br />


## 준비
docker, docker-compose 설치 [1편참고](/docker/) <br />
toolbox를 이용해 설치한 사람은  docker-compose를 따로 설치할 필요없다. <br />
codeigniter 3 보일러 플레이트 준비 [다운로드](https://codeigniter.com/download)

## 프로젝트 폴더 생성
\docker\jizero_member


## dockfile 작성
\docker\jizero_member\dockfile

### 각자 환경에 맞는 설치파일을 선택하여 추가&구성하자

```
FROM ubuntu:16.04

RUN sed -i 's/archive.ubuntu.com/mirror.kakao.com/g' /etc/apt/sources.list

RUN apt-get clean \
    && apt-get -y update \
    && apt-get install -y --no-install-recommends \
    locales \
    python-software-properties \
    software-properties-common \
    && locale-gen en_US.UTF-8 \
    && rm -rf /var/lib/apt/lists/*

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN add-apt-repository ppa:ondrej/php

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
      tzdata \
      apache2 \
      php7.3 \
      php7.3-cli \
      libapache2-mod-php7.3 \
      php7.3-gd \
      php7.3-json \
      php7.3-curl \
      php7.3-mbstring \
      php7.3-mysql \
      php7.3-redis \
      php7.3-mongodb \
      php7.3-xml \
      php7.3-xsl \
      php7.3-zip \
      composer \
      && rm -rf /var/lib/apt/lists/*



RUN ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime


COPY run /usr/local/bin/run
RUN chmod +x /usr/local/bin/run
RUN a2enmod rewrite

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf
RUN sed -i '/<Directory \/var\/www\/>/,/<\/Directory>/ s/AllowOverride None/AllowOverride all/' /etc/apache2/apache2.conf


COPY . /var/www/html

EXPOSE 80 443

CMD ["/usr/local/bin/run" ]


```


## docker-compose.yml 작성
\docker\jizero_member\docker-compose.yml

#### 컨테이너 두개를 만들것이다.  서비스명은 webservice /  mysqldb 임의로 정한다.

#### volumes에  www는 CI파일이 들어있는 루트 폴더이다.

```bash

version: '3'
services:
  webservice: ## 서비스명
    build: ./
    ports:
      - "8082:80"
    volumes:
      - ./www:/var/www/html ##{wwww} 연결시킬곳
    links:
      - mysqldb
  mysqldb: ## 서비스명
    image: mysql:5.7
    environment:
      - MYSQL_DATABASE=mysql ## 테이터베이스
      - MYSQL_ROOT_PASSWORD=jizero12 ##루트비번
      - MYSQL_USER=jizero ##사용자명
      - MYSQL_PASSWORD=jizero12 ## 연결시킬곳
    command: "--innodb_use_native_aio=0"
    volumes:
      - ./mysql_data:/var/lib/mysql
    ports:
      - "3306:3306"

```

## docker 실행 
```bash

docker-compose up

```


### container 구동 확인
```bash

docker ps

```
<img src="/assets/img/201909/php0.png" style="max-width:100%;">

툴박스를 깐 경우  Kitematic 으로 확인할수있다.
(초록불 확인!)
<img src="/assets/img/201909/php1.png" style="max-width:100%;">

<img src="/assets/img/201909/php2.png" style="max-width:100%;">


구동이되지않았을경우 에러로그를 잘살펴보자!

## 외부툴에서 실행시키기 (mysql workbench)

<img src="/assets/img/201909/php3.png" style="max-width:100%;">





## 프로젝트 종료

```bash

docker-compose down

```

## NEXT step
[2편에서는 CI로 restful api 서비스 만들기](/php_api/)
---
layout: post
title:  "[스터디 기록][2장] spring 5 recipes 2-6~2-10"
date:   2019-07-10 10:00
author: jizero
tags:	['springFramework',' spring recipes 5']
---


### 스프링 환경 및 프로파일마다 다른 POJO 로드하기

     @Profile 속성값으로 "" 안에 적되, 이름이 여러개면 csv형식 형식으로 {} 로 감싸 준다.

- **프로파일을 환경에 로드하기**
- 기본 프로파일 지정하기

### POJO에게 IOC 컨테이너 리소스 알려주기

- 빈이 Ioc 컨테이너 리소스를 인지하게 하려면 Aware 인터페이스를 구현한다

애네테이션을 활용해 애스팩트 지향 프로그래밍 하기

### 2-20 aspectj 애스팩트를 로드타임 위빙하기

[](https://www.notion.so/f2e50daae2704bda81bdbe511bb944b6#fbae27ec4cf6467e954a88424ed0b0cb)

AspectJ > 컴파일 타입 위빙 

ajc 전용 컴파일러가 담당

AspectJ > 로드 타입 위빙 (LTW)

로드타임 위빙용 에이전트

Spring > JVM 에 로드되는 시점에 위빙

@EnableLoadTimeWeaving

2-21 스프링에서 aspectj 애스팩트 구성하기

Aspects.aspectOf

2-22 aop를 이용해 pojo를 도메인 객체에 주입하기

2-23스프링 TaskExecutor로 동시성적용하기

2-24 POJO끼리 애플리케이션 이벤트 주고받기

이벤트발행

이벤트 리스너

@EventListener (스프링 4.2부터)

## 
매주 일요일 spring 5 recipes  정리본 
notion에 정리 중인 파일을 블로그에 옮긴글입니다.
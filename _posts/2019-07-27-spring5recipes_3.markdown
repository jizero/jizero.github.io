---
layout: post
title:  "[스터디 기록][3장] spring 5 recipes 3-1~3-5"
date:   2019-07-27 10:00
tags:	['springFramework',' spring recipes 5']
img:  201909/spring3_2.png # Add image post (optional)
---


## 3-1. 간단한 스프링 MVC 웹 애플리케이션 개발하기

스프링 MVC란
<img src="/assets/img/201909/spring3_1.png" />

**DispatcherServlet**

웹 브라우저로부터 송신된 Request를 일괄적으로 관리한다

**HandlerMapping**

RequestURL과 Controller 클래스의 맵핑을 관리한다.

**ViewResolver**(뷰 해석기)

Controller 클래스로부터 반환된 View 정보가 논리적인 View 이름일 경우에는 bean 설정파일에 정의되어 있는 ViewResolver 클래스를 이용하여 클라이언트에게 출력할 View 객체를 얻게 된다.

애플리케이션 설정

구성파일작성 ( gradle/ / maven )

Controller 작성

view작성 ( jstl / mastache .. )

웹애플리케이션 배포

## 3-2. @requestMapping에서 요청 매핑하기

<img src="/assets/img/201909/spring3_2.png" />

## 3-3. 핸들러 인터셉터로 요청 가로채기

## 3-4. 유저 로케일 해석하기

세션 속성에 따라 로케일 해석하기

쿠키에 따라 로케일 해석하기

## 3-5. 로케일별 텍스트 메시지 외부화 하기

스프링태그 라이브러리 사용하기

<spring:message>
## 
매주 일요일 spring 5 recipes  정리본 
notion에 정리 중인 파일을 블로그에 옮긴글입니다.
---
layout: post
title:  "react Enzyme 테스트"
date:   2019-05-20 10:00
author: jizero
tags:	['react','codeigniter']

---

## 목표
Enzyme을 이용한 react 테스트
## 준비
1.리액트 프로젝트 생성

```
npm install  -g create-react-app
create-react-app <프로젝트명>

```
<img src="/assets/img/201909/reacttest1.png" >


create-react-app에는 간단한 테스트기능이 내장되어있다.

<img src="/assets/img/201909/reacttest2.png" >

App.test.js 를 실행해보자
```
npm test  (또는 yarn test)

```
<img src="/assets/img/201909/reacttest3.png" >




## enzyme 사용해보기 
### enzyme 을 사용해 보기 위한 간단한 컴포넌트 생성

myname.js


```
import { mount } from 'enzyme';

```

shallow: 간단한 컴포넌트를 메모리 상에 렌더링. 단일 컴포넌트를 테스트 <br />
mount: HOC나 자식 컴포넌트까지 전부 렌더링합니다. 다른 컴포넌트와의 관계를 테스트할 때 유용 <br />
render: 컴포넌트를 정적인 html로 렌더링합니다. 



### 스냅샷 테스팅
### 컴포넌트 단위 테스팅
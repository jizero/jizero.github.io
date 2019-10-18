---
layout: post
title:  "[javascript] js 심층연구"
date:   2019-10-17 10:00
author: jizero
tags:	[javascript,vanilaJs,closure]


---
<style>
.page-cover-image { display:none; }
</style>
## 시작하며 
나 역시도 js를 jquery로 입문하게되면서  jquery 의존도가 몹시 높았다. <br />
최적화보다는 개발자의 편의성의 중요시된 jquery 라이브러리의 DOM관리는 그동안 많은 문제가 제기되었지만, <br />
이전에는  많은 개발자의 의존도와 하위브라우저 대응에대한 문제때문에 쉽게 버릴수 없는 상황이였다.<br />
최근 IE 8 이하 대응리스트에 거의 사라진 추세이며 이에 따른 성능을 고려한 순수 자바스크립트 (또는 정적타입) 필요성이 높아졌으며
자바스크립트 또한 깊은 이해를 필요로 하게 되었다. <br /> (굴지의 IT회사들은 이제 jquery를 쓰지 않는다고 하더라..)
이번기회에 자바스크립트에대한 심층 이해를 해보오자앗!

<del>(라고 쓰고 사실 .. javascript 어느정돈 다 알지 라는 생각을 갖고 있던 차에 보게 된 면접.. <br />
클로저와 스코프 문제들을 풀며 자괴감과 부끄러움에 뒤도안돌아보고 면접장을 빠져나오며 이를 갈고 심층 공부를 해보기로 ..)</del>

### 클로저
내가 알고 있던 개념
"내부함수가 외부함수의 맥락(context)에 접근할 수 있는 것"

```
function outter(){
     
    function inner(){
        var title = 'cccc';
        console.log(title);
    }
    inner();
}
outter();
```


### 클로저 심화
```
function makeCounter() {
  let count = 0;

  return function() {
    return count++; // has access to the outer "count"
  };
}

let counter = makeCounter();

alert( counter() ); // 0
alert( counter() ); // 1
alert( counter() ); // 2
```

그치만 객체를 추가한 경우에는 어떨까?

```
function makeCounter() {
  let count = 0;

  return function() {
    return count++;
  };
}

let counter = makeCounter();
let counter2 = makeCounter();
let counter3 = counter;

console.log( counter() ); // 0
console.log( counter() ); // 1

console.log( counter2() ); // ?
console.log( counter2() ); // ?
console.log( counter3() ); // ?

```

counter3은  counter를 공유하므로 카운터는 2
클로저는(이 예제에서 내부의 익명함수) 외부 변수에 대해 값이 아닌 참조로 접근한다.


### 프로토타입 

---|:---:|---:
Prototype Object| 함수를 정의하면 생성되는 객체
Prototype Link (__proto__)|  자신을 만들어낸 객체의 원형을 참조
Constructor |함수를 정의하면 부여되는 생성자 자격 new 키워드를 이용해 객체를 만들어낼 수 있음


<br />
```
function rects (w, h) {
    this.width = w;
    this.height = h;
    this.get_area = function () { 
        return this.width * this.height;
    }
};

var rect = new rects(10, 15);

```

### 프로토타입 심화
 프로토타입 체인은 하위 객체에서 상위객체의 프로퍼티와 메소드를 상속받는다.

<br />
```
//1번
function rects (w, h) {
    this.width = w;
    this.height = h;
    this.get_area = function () { 
        return this.width * this.height;
    }
};


//2번
function rects2 (w, h) {
    this.width = w;
    this.height = h;
};

 rects2.prototype.get_area = function () { 
        return this.width * this.height;
 }

var rect = new rects(10, 15);
var rect2 = new rects2(10, 15);

 rect.get_area = function () { 
        return this.width + this.height;
 }

 rects2.prototype.get_area = function () { 
        return this.width + this.height;
 }

var rect3 = new rects(10,16);
var rect4 = new rects2(10,16);

console.log(rect.get_area());
console.log(rect2.get_area());
console.log(rect3.get_area());
console.log(rect4.get_area());

```
1번
<img src="/assets/img/201910/201910081.PNG" />

2번
<img src="/assets/img/201910/201910082.PNG" />



1번과 2번은 무엇이 다른가?
2의 Prototype Object의 get_area 메소드를 재정의 하였을 때 rect4 객체도 그 영향을 받는다는 것

```
rect1  // 25
rect2  // 25
rect3  // 160
rect4  // 26


```



### 참고
https://beizix.tistory.com/entry/자바스크립트-Function-의-비밀-prototype-과-new [절대적이고 상대적인 Spring Boot 이야기] <br />
http://insanehong.kr/post/javascript-prototype/ - Javascript 기초 - Object prototype 이해하기
 








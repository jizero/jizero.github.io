---
layout: post
title:  "[codility] MaxNonoverlappingSegments"
date:   2019-10-01 10:00
author: jizero
tags:	[javascript,codility,algorithm]

---

## 문제 요약
배열 A B 와 선분을 만들어 겹치지 않는 선을 찾는 문제<br />
문제 이해만 30분 소요 ㅜㅜ  ** 탐욕적 알고리즘일 알아야하는게 핵심!
<br />
input : <br />
 A = {1,3,7,9,9}<br />
 B = {5,6,8,9,10}<br />

<img src="/assets/img/201910/code1.PNG" />
<br />
output : 3


### 나의코드 50% 

```javascript

function solution(A, B) {
    // write your code in JavaScript (Node.js 8.9.4)
    let resultCount = 0;
    let segLen =  A.length;
    for(let i=0; i < A.length ;i++){

        if(B[i] >= A[i+1] &&  B[i] <= B[i+1]){
            resultCount++;
        }
    }
    

    return (segLen -resultCount);
}

```
* 예외처리의 누락
* 총 선분(배열길이) 을 구한후 중복되지 않는 부분을 제거하였으나 에러검출 4개..




### 100% code 
```javascript
function solution(A, B) {
    // write your code in JavaScript (Node.js 8.9.4)
    if (A.length <= 1) {
        return A.length;
    }
    //배열 길이체크가 10%

    let resultCount = 1;
    let prevEnd = B[0];
    for(let i=1; i < A.length ;i++){
        if(A[i] > B[i+1]  ||  A[i] > prevEnd){
            resultCount++;
             prevEnd = B[i];
        }
    }
    

    return resultCount;
}
```

### 그리드 알고리즘 학습 후 스스로 다시 푼 문제
```javascript
// you can write to stdout for debugging purposes, e.g.
// console.log('this is a debug message');

function solution(A, B) {
    // write your code in JavaScript (Node.js 8.9.4)
    let result = '';
 
    if(A.length < 1) {
          return 0;
    }
    
    var count = 1;
    var key = 0;
    for ( let i = 0; i < A.length; i++ ){
        if(K[key] < A[i]){
            count++;
            key = i;
        }   
    }
 
    
    return count;
}

````
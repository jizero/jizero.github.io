---
layout: post
title:  "[codility] GenomicRangeQuery"
date: 2020-08-27 10:00
author: jizero
tags:	[javascript,codility,algorithm]

---

## 문제 요약
GenomicRangeQuery

특정범위에서 최소값 찾기



### 1차시도  (처음으로 1차시도만에 100%를 받아본 코드)
[https://app.codility.com/demo/results/trainingADRGB9-ADP/](https://app.codility.com/demo/results/trainingADRGB9-ADP/)
```javascript
// you can write to stdout for debugging purposes, e.g.
// console.log('this is a debug message');

// console.log('this is a debug message');

function solution(S, P, Q) {
    // write your code in JavaScript (Node.js 8.9.4)

    let start = 0;
    let stop = 0;

    let prefixSum = []; 
    let str = [];
    for(let i =0; i < P.length; i++) {

        start = (P[i]);
        stop = (Q[i]+1);
        str = S.substring(start,stop);

        if(str.indexOf("A") !== -1){
           prefixSum.push(1);
        }else if(str.indexOf("C")!== -1){
            prefixSum.push(2);
        }else if(str.indexOf("G") !== -1){            
            prefixSum.push(3);
        }else if(str.indexOf("T") !== -1){            
            prefixSum.push(4)
        }

    }

    return prefixSum;
}

```

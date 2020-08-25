---
layout: post
title:  "[codility] 
CyclicRotation"
date:   2020-08-025 10:00
author: jizero
tags:	[javascript,codility,algorithm]

---

## 문제 요약
CyclicRotation
START
Rotate an array to the right by a given number of steps.
<br />
input : <br />
   A = [3, 8, 9, 7, 6]<br />
    K = 3 <br />


<br />
output : [9, 7, 6, 3, 8]


### 1차시도 나의코드 87% 
https://app.codility.com/demo/results/training5BZFRG-CE7/
```javascript
function solution(A, K) {
    // write your code in JavaScript (Node.js 8.9.4)
    let arr = [];
    for(let i =0; i < K; i++) {
        const ele = A.pop();
        A.unshift(ele);
    }
  return A;

}

```
* 




### 100% code 
https://app.codility.com/demo/results/trainingFGNXP3-DFS/(https://app.codility.com/demo/results/trainingFGNXP3-DFS/)
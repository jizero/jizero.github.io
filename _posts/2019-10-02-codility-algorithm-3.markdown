---
layout: post
title:  "[codility] FrogRiverOne"
date:   2019-10-02 10:00
author: jizero
tags:	[javascript,codility,algorithm]

---

## 문제 요약
배열 A에서 주어진 X까지 순차적으로 다 나온 배열인덱스를 리턴해주기 없을경우 -1

input :  A = {3,1,2,4,3} <br />
         X = 5
<br />
  A[0] = 1 <br />
  A[1] = 3 <br />
  A[2] = 1 <br />
  A[3] = 4 <br />
  A[4] = 2 <br />
  A[5] = 3 <br />
  A[6] = 5 <br />
  A[7] = 4
<br /><br />
output : 6


### 나의코드 72%  O(N ** 2)

```javascript
function solution(X, A) {
    // write your code in JavaScript (Node.js 8.9.4)
    let result = -1;
    let resultArr = [];
    let arrIdx = 0;
    for(let i=0;i < A.length; i++ ){
        if(X >= A[i]){
            if (resultArr.indexOf(A[i]) < 0 ){ 
                resultArr.push(A[i]);
            }
            if(resultArr.length == X){
                      result= i;
                      break
             }
        }
    }
    
    return result;

}

```
* 중복제거를 indexOf 사용함으로써 복잡도 증가.. 


* 중복제거를따로 하지않고 배열인덱스를 사용하여 100%로..
### 100% code  

```javascript
function solution(X, A) {
    // write your code in JavaScript (Node.js 6.4.0) 

    let sequence = [0];
    let position = -1;
    let counter = 0;

    if (X === 1 && A[0] === 1)
        return 0;

    for (let i = 0; i <= A.length - 1; i++) {

        if (A[i] <= X) {
            if (!sequence[A[i]]) {
                counter++;
            }
            
            sequence[A[i]] = A[i];

            if (counter === X) {
                position = i;
                break;
            }
        }
    }
    return position;
}

```

* 이번코드의경우 자바로 할경우 훨씬 간결하여 자바코드도 가져와보았다

```java
// you can also use imports, for example:
import java.util.*;

// you can write to stdout for debugging purposes, e.g.
// System.out.println("this is a debug message");

class Solution {
    public int solution(int X, int[] A) {
        Set<Integer> per = new HashSet<>();
        for(int i=0; i<A.length; i++) {
            if(A[i] <= X) per.add(A[i]);
            if(per.size() == X) return i;
        }
        return -1;
    }
}
```
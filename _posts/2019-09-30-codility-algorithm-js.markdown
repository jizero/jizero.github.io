---
layout: post
title:  "[codility] TapeEquilibrium"
date:   2019-09-30 10:00
author: jizero
tags:	[javascript,codility,algorithm]

---

## 문제 요약
포인터위치에따라 배열을 나누어 합들을 구한 후 최소값을 찾는 문제

input :  A = {3,1,2,4,3}

p = 1 => 3 - (1+2+4+3) <br />
p = 2 => (3+1) - (2+4+3) <br />
p = 3 => (3+1+2) - (4+3) <br />
p = 4 =>  (3+1+2+4) - 3 <br />

output : 1


### 나의코드 53% 

```javascript
function solution(A) {

    let aNum = 0;
    let resultArr = [];
    let  tmpArr = A;

    for(i=0; i< (A.length-1) ; i++){
        let pNum = 0;
        aNum += A[i]
        tmpArr[i] = 0
        pNum = tmpArr.reduce((a, b) => a + b, 0); //여기가 문제였던듯
        resultArr.push(Math.abs(aNum-pNum));
    }

    return Math.min.apply(null, resultArr);

}

```
* 방향은 비슷하였으나 오른쪽 배열을 구하는데 for문안에 reduce를 써서 복잡도가 늘어난 상황




### 100% code  (https://gist.github.com/jeanlescure/797eef515cfa4a05830b)
```javascript
function solution(A) {
    var retval;
    
    var sumRight = A.reduce(function(pv, cv, idx){ return (idx > 0)? pv + cv : 0; }, 0);
    var sumLeft = 0;
    var substractions = [];
    var maxI = A.length - 1;
    
    for(var i = 0; i < maxI; i++){
        sumLeft += A[i];
        substractions.push(Math.abs(sumLeft - sumRight));
        if (i + 1 <= maxI) sumRight -= A[i + 1];
    }
    
    return substractions.reduce(function(pv,cv,idx){ return (idx > 0)? ((pv < cv)? pv : cv) : cv; }, 0);
}

```
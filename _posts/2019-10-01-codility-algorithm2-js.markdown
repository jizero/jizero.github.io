---
layout: post
title:  "[codility] FloodDepth"
date:   2020-08-22 10:00
author: jizero
tags:	[javascript,codility,algorithm]

---

## 문제 요약
엄청난 비가 내린 후 산의 최대 수심을 찾으십시오.
<br />

input :    <br />
    A[0] = 1 <br />
    A[1] = 3 <br />
    A[2] = 2 <br />
    A[3] = 1 <br />
    A[4] = 2 <br />
    A[5] = 1 <br />
    A[6] = 5 <br />
    A[7] = 3 <br />
    A[8] = 3 <br />
    A[9] = 4 <br />
    A[10] = 2 <br />
<br />
output : 3 <br />
<br /><br />

### 100% code 
```javascript
function solution(A) {
    // write your code in JavaScript (Node.js 8.9.4)
    if (A.length  <= 2 ){
        return 0;
    }
    let h = 0;
    let r = 0;
    let max = 0;
    let cnt = 0;
    for (let i=1; i < (A.length); i++) {
        if(A[i] > A[h]){
             cnt= (A[h]-A[r]);
             h = i;
             r = h;
           //  console.log('111 '+cnt);
        } else if(A[i] > A[r]) {
            cnt= (A[i]-A[r]);
            //console.log('222 '+cnt);
        } else if(A[i] < A[r]) {            
            r = i;
                 // console.log('low'+cnt);
        } 
        

        
       if(max < cnt){
           max = cnt;
       }
    }
    
    return max;
}
}
```


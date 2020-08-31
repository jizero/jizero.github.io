---
layout: post
title:  "[프로그래머스] Lev.2 조이스틱"
date: 2020-08-31 10:00
author: jizero
tags:	[javascript,programmers,algorithm]

---

## 문제 요약
조이스틱으로 알파벳 이름을 완성하세요. 맨 처음엔 A로만 이루어져 있습니다.
ex) 완성해야 하는 이름이 세 글자면 AAA, 네 글자면 AAAA


## 나의코드
```javascript
function solution(name) {
    let firstChar = 65;
    let lastChar = 90;
    
    let answer = 0,a_count = 0; //A갯수 체크
    let up= 0,down= 0,left= 0,right = 0 ,move = 0;

    for(let i= 0; i < name.length; i++) {
        //up down 횟수체크
        up = name.charCodeAt(i) - firstChar;
        down =  (lastChar - name.charCodeAt(i)) +1;
        if(up == 0  ) {
            a_count++;
        }else{
            if(up > down) {
               answer += down ;
            }else{
               answer += up
            }
            //move!! 좌우 확인
            if(i == a_count){
                left = a_count;
                right = 1;
            } else {
                left = 1+a_count;
                right = i-a_count;
            }
          
            if(left <= right) {
                answer += left;
            } else {
                answer += right;
            }
            a_count = 0;
        }
    }

    //예외처리1
    if(left > right && name.charAt(name.length-1)== "A"){
        move = move+1;
    }
    //예외처리2
    if(left < right && a_count>0){
        answer += a_count;
    }
    return (answer + move);
}
```

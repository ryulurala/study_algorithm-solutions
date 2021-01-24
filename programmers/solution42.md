---
title: "다트 게임"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[다트 게임](https://programmers.co.kr/learn/courses/30/lessons/17682)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

// 0~10 정수, 문자 S, D, T, *, #
// S, D, T : 1제곱, 2제곱, 3제곱
// * 스타상: 바로 전에 얻은 점수 2배
// # 아차상: 해당 점수 마이너스

int solution(string dartResult) {
    int answer = 0;

    vector<int> v;
    int num = 0;
    for(int i=0; i<dartResult.length(); i++){
        char c = dartResult[i];
        if(c>='0' && c<='9'){
            v.push_back(num);   // 이전 점수 push, 처음은 0
            if(c=='1' && dartResult[i+1]=='0') {
                num = 10;
                i++;    // 다음 정수 문자 skip
            }
            else num = c - '0';
        }
        else if(c=='D') num *= num;
        else if(c=='T') num *= num*num;
        else if(c=='*'){
            v.back() *= 2;
            num *= 2;
        }
        else if(c=='#') num *= (-1);
    }
    v.push_back(num);   // 마지막 점수 push

    for(auto e: v) answer+=e;   // 점수 합

    return answer;
}
```

### JavaScript

```js
function solution(dartResult) {
  var answer = 0;

  const scores = [];
  let num = 0;

  for (let i = 0; i < dartResult.length; i++) {
    const ch = dartResult[i];
    if (ch >= "0" && ch <= "9") {
      scores.push(num); // 이전 점수 push
      if (ch == "1" && dartResult[i + 1] == "0") {
        num = 10; // 현재 점수
        i++; // 다음 정수 문자 skip
      } else {
        num = ch - "0"; // 현재 점수
      }
    } else if (ch == "D") {
      num *= num;
    } else if (ch == "T") {
      num *= num * num;
    } else if (ch == "*") {
      scores[scores.length - 1] *= 2;
      num *= 2;
    } else if (ch == "#") {
      num = -num;
    }
  }
  scores.push(num); // 마지막 점수 push

  scores.some((value) => {
    answer += value; // 점수 합치기
  });

  return answer;
}
```

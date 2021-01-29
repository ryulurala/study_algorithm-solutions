---
title: "가운데 글자 가져오기"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-19"
---

## 문제 링크

[가운데 글자 가져오기](https://programmers.co.kr/learn/courses/30/lessons/12903)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

string solution(string s) {
    string answer = "";

    int center = s.length()/2;
    if(s.length()%2==0){
        // 길이가 짝수일 때
        answer = s.substr(center-1, 2);
    }
    else{
        // 길이가 홀수일 때
        answer = s[center];
    }
    return answer;
}
```

### JavaScript

```js
function solution(s) {
  var answer = "";

  let center = Math.floor(s.length / 2); // 정수로 반환

  if (s.length % 2 == 0) {
    // 길이가 짝수일 때
    answer = s.substring(center - 1, center + 1);
  } else {
    // 길이가 홀수일 때
    answer = s[center];
  }

  return answer;
}
```

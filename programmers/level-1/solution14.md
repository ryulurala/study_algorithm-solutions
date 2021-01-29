---
title: "문자열 내 p와 y의 개수"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-19"
---

## 문제 링크

[문자열 내 p와 y의 개수](https://programmers.co.kr/learn/courses/30/lessons/12916)

### C++

```cpp
#include <string>
#include <iostream>

using namespace std;

bool solution(string s)
{
    bool answer = true;
    int base = 0;   // 기준점

    for(char c: s){
        if(c == 'P' || c == 'p') base++;
        else if(c == 'Y' || c == 'y') base--;
    }

    answer = base == 0 ? true : false;

    return answer;
}
```

### JavaScript

```js
function solution(s) {
  var answer = true;

  let base = 0; // 기준
  s = s.toLowerCase(); // 소문자로 변환
  console.log(s);
  for (let i = 0; i < s.length; i++) {
    if (s[i] == "p") base++;
    else if (s[i] == "y") base--;
  }

  answer = base == 0 ? true : false;

  return answer;
}
```

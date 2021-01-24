---
title: "자릿수 더하기"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[자릿수 더하기](https://programmers.co.kr/learn/courses/30/lessons/12931)

### C++

```cpp
#include <iostream>
#include <string>

using namespace std;
int solution(int n)
{
    int answer = 0;

    string s = to_string(n);
    for(char c: s){
        answer += c - '0';
    }

    return answer;
}
```

### JavaScript

```js
function solution(n) {
  var answer = 0;

  answer = n
    .toString()
    .split("")
    .reduce((prev, value) => {
      return prev * 1 + value * 1;
    }, 0);

  return answer;
}
```

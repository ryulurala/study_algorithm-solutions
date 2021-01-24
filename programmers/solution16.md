---
title: "문자열 다루기 기본"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[문자열 다루기 기본](https://programmers.co.kr/learn/courses/30/lessons/12918)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

bool solution(string s) {
    bool answer = true;

    if(s.length()==4 || s.length()==6){
        for(char c: s){
            if(c >= '0' && c <= '9') continue;
            answer = false;
            break;
        }
    }
    else{
        answer = false;
    }

    return answer;
}
```

### JavaScript

```js
function solution(s) {
  var answer = true;

  if (s.length == 4 || s.length == 6) {
    for (let i = 0; i < s.length; i++) {
      if (s[i] >= "0" && s[i] <= "9") continue;
      answer = false;
      break;
    }
  } else {
    answer = false;
  }

  return answer;
}
```

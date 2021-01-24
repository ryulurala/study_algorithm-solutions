---
title: "콜라츠 추측"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[콜라츠 추측](https://programmers.co.kr/learn/courses/30/lessons/12943)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

int solution(int num) {
    int answer = 0;
    long numLong = num;     // int 범위 초과

    for(int i=0; i<500; i++){
        if(numLong==1) break;
        numLong = numLong&1 ? numLong*3+1 : numLong/2;
        answer++;
    }
    answer = answer==500 ? -1 : answer;

    return answer;
}
```

### JavaScript

```js
function solution(num) {
  var answer = 0;

  for (let i = 0; i < 500; i++) {
    if (num === 1) break;
    num = num & 1 ? num * 3 + 1 : num / 2;
    answer++;
  }
  answer = answer === 500 ? -1 : answer;

  return answer;
}
```

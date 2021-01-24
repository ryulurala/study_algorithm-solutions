---
title: "두 정수 사이의 합"
excerpt: "프로그래머스 풀이"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
toc: true
toc_sticky: true
---

## 문제 링크

[두 정수 사이의 합](https://programmers.co.kr/learn/courses/30/lessons/12912)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

long long solution(int a, int b) {
    long long answer = 0;

    if(a > b){  // a가 크면
        for(int i=b; i<=a; i++){
            answer += i;
        }
    }
    else if(a < b){     // a가 작으면
        for(int i=a; i<=b; i++){
            answer += i;
        }
    }
    else {      // 같으면
        answer = a;
    }

    return answer;
}
```

### JavaScript

```js
function solution(a, b) {
  var answer = 0;

  if (a > b) {
    for (let i = b; i <= a; i++) {
      // a가 클 경우
      answer += i;
    }
  } else if (a < b) {
    for (let i = a; i <= b; i++) {
      // b가 클 경우
      answer += i;
    }
  } else {
    // 같을 경우
    answer = a;
  }

  return answer;
}
```

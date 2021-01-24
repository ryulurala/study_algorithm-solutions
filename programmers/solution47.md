---
title: "멀쩡한 사각형"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-2]
toc: true
toc_sticky: true
---

## 문제 링크

[멀쩡한 사각형](https://programmers.co.kr/learn/courses/30/lessons/62048)

### C++

```cpp
using namespace std;

long long gcd(long long a, long long b){
    if(a%b == 0) return b;
    return gcd(b, a%b);
}

long long solution(int w,int h) {
    long long answer = 1;
    answer = w*h - (w+h-gcd(w,h));
    return answer;
}
```

### JavaScript

```js
function solution(w, h) {
  var answer = 1;

  const gcd = (a, b) => {
    if (a % b === 0) return b;
    return gcd(b, a % b);
  };

  answer = w * h - (w + h - gcd(w, h));

  return answer;
}
```

---
title: "최대공약수와 최소공배수"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[최대공약수와 최소공배수](https://programmers.co.kr/learn/courses/30/lessons/12940)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

int func(int a, int b){
    if(a % b == 0) return b;
    return func(b, a % b);  // 나누어떨어질 때까지 재귀
}

vector<int> solution(int n, int m) {
    vector<int> answer;

    answer.push_back(func(n, m));       // 최대공약수
    answer.push_back(n*m/answer[0]);    // 최소공배수

    return answer;
}
```

### JavaScript

```js
function solution(n, m) {
  var answer = [];

  const func = (a, b) => {
    if (a % b === 0) return b;
    return func(b, a % b);
  };

  answer.push(func(n, m)); // 최대공약수
  answer.push((n * m) / answer[0]); // 최소공배수

  return answer;
}
```

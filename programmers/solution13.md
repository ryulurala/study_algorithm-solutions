---
title: "문자열 내 마음대로 정렬하기"
excerpt: "프로그래머스 풀이"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
toc: true
toc_sticky: true
---

## 문제 링크

[문자열 내 마음대로 정렬하기](https://programmers.co.kr/learn/courses/30/lessons/12915)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int base;   // 인덱스 기준

bool cmp(string a, string b){
    if(a[base] == b[base]) return a < b;
    return a[base] < b[base];
}

vector<string> solution(vector<string> strings, int n) {
    vector<string> answer(strings);

    base = n;   // 인덱스 지정
    sort(answer.begin(), answer.end(), cmp);

    return answer;
}
```

### JavaScript

```js
function solution(strings, n) {
  var answer = [];

  answer = strings.slice(); // 깊은 복사
  answer.sort((a, b) => {
    if (a[n] == b[n]) {
      // 사전 정렬
      return a < b ? -1 : a === b ? 0 : 1;
    } else {
      // 인덱스 사전 정렬
      return a[n] < b[n] ? -1 : a === b ? 0 : 1;
    }
  });

  return answer;
}
```

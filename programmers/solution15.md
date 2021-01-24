---
title: "문자열 내림차순으로 배치하기"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[문자열 내림차순으로 배치하기](https://programmers.co.kr/learn/courses/30/lessons/12917)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

string solution(string s) {
    string answer(s);

    sort(answer.rbegin(), answer.rend());   // 내림차순 정렬

    return answer;
}
```

### JavaScript

```js
function solution(s) {
  var answer = "";

  answer = s
    .split("") // 배열로 변환
    .sort((a, b) => {
      // 사전 반대 정렬
      if (a > b) return -1;
      else return 1;
    })
    .join(""); // string으로 변환

  console.log(answer);

  return answer;
}
```

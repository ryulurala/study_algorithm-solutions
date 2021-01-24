---
title: "자연수 뒤집어 배열로 만들기"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[자연수 뒤집어 배열로 만들기](https://programmers.co.kr/learn/courses/30/lessons/12932)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(long long n) {
    vector<int> answer;

    while(true){
        if(n == 0) break;
        answer.push_back(n%10);
        n/=10;
    }

    return answer;
}
```

### JavaScript

```js
function solution(n) {
  var answer = [];

  while (true) {
    if (n === 0) break;
    answer.push(n % 10);
    n = parseInt(n / 10);
  }

  return answer;
}
```

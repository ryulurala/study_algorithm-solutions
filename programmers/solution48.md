---
title: "124 나라의 숫자"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-2]
toc: true
toc_sticky: true
---

## 문제 링크

[124 나라의 숫자](https://programmers.co.kr/learn/courses/30/lessons/12899)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

string solution(int n) {
    string answer = "";

    string oneTwoFour= "124";

    while(n>0){
        answer += oneTwoFour[(n-1)%3];
        n = (n-1)/3;
    }
    reverse(answer.begin(), answer.end());  // 뒤집기

    return answer;
}
```

### JavaScript

```js
function solution(n) {
  var answer = "";

  while (n > 0) {
    answer += "124"[parseInt((n - 1) % 3)];
    n = parseInt((n - 1) / 3);
  }
  answer = answer.split("").reverse().join(""); // 뒤집기

  return answer;
}
```

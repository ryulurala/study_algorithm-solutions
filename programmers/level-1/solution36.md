---
title: "핸드폰 번호 가리기"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-20"
---

## 문제 링크

[핸드폰 번호 가리기](https://programmers.co.kr/learn/courses/30/lessons/12948)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

string solution(string phone_number) {
    string answer = "";

    for(int i=0; i<phone_number.length()-4; i++)
        answer += '*';
    for(int i=phone_number.length()-4; i<phone_number.length(); i++)
        answer += phone_number[i];

    return answer;
}
```

### JavaScript

```js
function solution(phone_number) {
  var answer = "";

  for (let i = 0; i < phone_number.length - 4; i++) answer += "*";
  for (let i = phone_number.length - 4; i < phone_number.length; i++)
    answer += phone_number[i];

  return answer;
}
```

---
title: "짝지어 제거하기"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-01"
---

## 문제 링크

[짝지어 제거하기](https://programmers.co.kr/learn/courses/30/lessons/12973)

### C++

```cpp
#include <iostream>
#include <string>

using namespace std;

int solution(string s) {
    int answer = 0;

    string str="";
    str+=s[0];
    for(int i=1; i<s.length(); i++){
        if(str.back()==s[i]) str.pop_back();
        else str+=s[i];
    }

    if(str.empty()) answer=1;

    return answer;
}
```

### JavaScript

```js
function solution(s) {
  var answer = 0;

  const stack = [];
  stack.push(s[0]);
  for (let i = 1; i < s.length; i++) {
    if (stack[stack.length - 1] === s[i]) stack.pop();
    else stack.push(s[i]);
  }

  if (stack.length === 0) answer = 1;

  return answer;
}
```

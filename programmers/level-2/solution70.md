---
title: "올바른 괄호"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-30"
---

## 문제 링크

[올바른 괄호](https://programmers.co.kr/learn/courses/30/lessons/12909)

### C++

```cpp
#include <string>
#include <iostream>

using namespace std;

bool solution(string s){
    bool answer = true;

    int check=0;
    for(char ch: s){
        if(ch=='(') check++;
        else if(ch==')') check--;
        if(check<0) break;
    }
    answer=(check==0)?true:false;

    return answer;
}
```

### JavaScript

```js
function solution(s) {
  var answer = true;

  let cnt = 0;
  s.split("").some((val) => {
    if (val === "(") cnt++;
    else if (val === ")") cnt--;
    if (cnt < 0) return true; // break;
  });

  answer = cnt === 0 ? true : false;

  return answer;
}
```

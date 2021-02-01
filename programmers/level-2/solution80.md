---
title: "JadenCase 문자열 만들기"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-01"
---

## 문제 링크

[JadenCase 문자열 만들기](https://programmers.co.kr/learn/courses/30/lessons/12951)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

string solution(string s) {
    string answer = "";

    answer+=toupper(s[0]);  // 처음 대문자(공백이면 공백)
    for(int i=1; i<s.length(); i++){
        if(s[i-1]!=' ') answer+=tolower(s[i]);
        else answer+=toupper(s[i]);     // ' '이면 그다음 대문자
    }

    return answer;
}
```

### JavaScript

```js
function solution(s) {
  var answer = "";

  answer = s
    .toLowerCase()
    .split(" ")
    .map((val) => {
      return val.replace(/[a-z]/, (v, i) => {
        if (i === 0) return v.toUpperCase();
        else return v;
      });
    })
    .join(" ");

  return answer;
}
```

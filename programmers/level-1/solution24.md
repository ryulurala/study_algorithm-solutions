---
title: "이상한 문자 만들기"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-20"
---

## 문제 링크

[이상한 문자 만들기](https://programmers.co.kr/learn/courses/30/lessons/12930)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

string solution(string s) {
    string answer = "";

    int count = 0;
    for(char c: s){
        if(c == ' '){
            count = 0;
        }
        else{
            if(count%2!=0) c = tolower(c);
            else c = toupper(c);
            count++;
        }
        answer += c;
    }

    return answer;
}
```

### JavaScript

```js
function solution(s) {
  var answer = "";

  answer = s
    .split(" ")
    .map((value, index, array) => {
      let str = "";
      for (let i = 0; i < value.length; i++) {
        if (i % 2 === 0) {
          str += value[i].toUpperCase();
        } else {
          str += value[i].toLowerCase();
        }
      }
      return str;
    })
    .join(" ");

  return answer;
}
```

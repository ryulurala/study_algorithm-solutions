---
title: "시저 암호"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[시저 암호](https://programmers.co.kr/learn/courses/30/lessons/12926)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

string solution(string s, int n) {
    string answer = "";

    for(int i=0; i<s.length(); i++){
        char c = s[i];
        if(c >= 'A' && c <= 'Z'){
            if(c+n <= 'Z') c += n;
            else c += n-26;
        }
        else if(c >= 'a' && c <= 'z'){
            if(c+n <= 'z') c += n;
            else c += n-26;
        }
        answer += c;
    }

    return answer;
}
```

### JavaScript

```js
function solution(s, n) {
  var answer = "";

  let upper = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
  let lower = upper.toLowerCase();

  for (let i = 0; i < s.length; i++) {
    let c = s[i];
    if (c >= "A" && c <= "Z") {
      c = upper[(upper.indexOf(c) + n) % upper.length];
    } else if (c >= "a" && c <= "z") {
      c = lower[(lower.indexOf(c) + n) % lower.length];
    }
    answer = answer.concat(c);
  }

  return answer;
}
```

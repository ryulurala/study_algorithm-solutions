---
title: "괄호 변환"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-2]
toc: true
toc_sticky: true
---

## 문제 링크

[괄호 변환](https://programmers.co.kr/learn/courses/30/lessons/60058)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

// '(', ')' 개수 같으면 균형잡힌 괄호 문자열
// 짝도 맞으면 올바른 괄호 문자열

string solution(string p) {
    string answer = "";

    if(p=="") return "";    // 빈 문자열 반환
    else{
        int base=0;
        int index=0;
        for(char ch: p){
            // u, v분리
            if(ch=='(') base++;
            else if(ch==')') base--;
            if(base==0) break;
            index++;
        }
        string u = p.substr(0, index+1);    // u
        string v = p.substr(index+1);   // v

        bool isRight = true;
        for(char ch: u){
            // u 검사
            if(ch=='(') base++;
            else if(ch==')') base--;
            if(base>=0) continue;
            isRight = false;
            break;
        }

        if(isRight) answer += u + solution(v);  // 올바른 괄호 문자열
        else{
            // Only. 균형잡힌 문자열
            answer += '('+solution(v)+')';
            u.erase(u.begin());
            u.pop_back();

            for(char& ch: u){
                // 괄호 방향 바꾸기
                if(ch=='(') ch=')';
                else if(ch==')') ch='(';
            }

            answer += u;
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(p) {
  var answer = "";

  if (p == "") {
    return "";
  } else {
    let base = 0;
    let index = 0;
    while (index < p.length) {
      if (p[index] === "(") base++;
      else if (p[index] === ")") base--;
      if (base === 0) break;
      index++;
    }
    let u = p.substring(0, index + 1); // u
    let v = p.substring(index + 1); // v

    let isRight = true;
    for (let i = 0; i < u.length; i++) {
      // u 검사
      if (u[i] === "(") base++;
      else if (u[i] === ")") base--;
      if (base < 0) {
        isRight = false;
        break;
      }
    }

    if (isRight) {
      // 올바른 괄호 문자열
      answer += u + solution(v);
    } else {
      // 올바른 괄호 문자열 X
      answer += "(" + solution(v) + ")";
      u = u.substring(1, u.length - 1);
      u = u.replace(/\(/g, "#");
      u = u.replace(/\)/g, "(");
      u = u.replace(/\#/g, ")");

      answer += u;
    }
  }

  return answer;
}
```

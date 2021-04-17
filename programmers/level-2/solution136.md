---
title: "괄호 회전하기"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-04-17"
---

## 문제 링크

[괄호 회전하기](https://programmers.co.kr/learn/courses/30/lessons/76502)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

int solution(string s) {
    int answer = 0;

    for(int i=0; i<s.length(); i++){

        vector<char> stk;
        for(char ch: s){
            if(stk.empty() || ch=='(' || ch=='{' || ch=='[')
                stk.push_back(ch);
            else if(ch==')' && stk.back()=='(')
                stk.pop_back();
            else if(ch=='}' && stk.back()=='{')
                stk.pop_back();
            else if(ch==']' && stk.back()=='[')
                stk.pop_back();
            else
                break;
        }

        // 올바른지
        if(stk.empty()) answer++;

        // 회전
        char ch = s.front();
        s.erase(s.begin());
        s.push_back(ch);
    }

    return answer;
}
```

### JavaScript

```js
function solution(s) {
  var answer = 0;

  const sLen = s.length;
  for (let i = 0; i < sLen; i++) {
    const stack = [];
    s.split("").forEach((v) => {
      if (stack.length === 0) stack.push(v);
      else if (v === ")" && stack[stack.length - 1] === "(") stack.pop();
      else if (v === "}" && stack[stack.length - 1] === "{") stack.pop();
      else if (v === "]" && stack[stack.length - 1] === "[") stack.pop();
      else stack.push(v);
    });

    // 올바른지
    if (stack.length === 0) answer++;

    // 회전
    s = s
      .split("")
      .map((v, i, arr) => arr[(i + 1) % sLen])
      .join("");
  }

  return answer;
}
```

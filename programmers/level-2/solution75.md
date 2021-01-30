---
title: "이진 변환 반복하기"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-31"
---

## 문제 링크

[이진 변환 반복하기](https://programmers.co.kr/learn/courses/30/lessons/70129)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(string s) {
    vector<int> answer(2, 0);

    while(true){
        answer[0]++;
        int len=0;
        for(char ch: s) (ch=='1')?len++:0;
        answer[1]+=(s.length()-len);

        if(len==1) break;

        // 길이 -> 이진수
        s="";
        while(len>0){
            if(len&1) s+='1';
            else s+='0';
            len>>=1;
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(s) {
  var answer = [0, 0];

  while (true) {
    const prev = s.length;
    const next = s.replace(/0/g, "").length;

    answer[0]++; // 횟수
    answer[1] += prev - next; // 0 갯수

    if (next === 1) break;
    s = next.toString(2); // 길이 -> 이진수
  }

  return answer;
}
```

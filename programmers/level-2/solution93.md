---
title: "압축"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-03"
---

## 문제 링크

[압축](https://programmers.co.kr/learn/courses/30/lessons/17684)

### C++

```cpp
#include <string>
#include <vector>
#include <map>

using namespace std;

vector<int> solution(string msg) {
    vector<int> answer;

    // init
    map<string, int> dict;
    int index=0;    // 색인 번호
    while(index<26){
        string str(1, 'A'+index);
        dict[str]=++index;
    }

    for(int i=0; i<msg.length();){
        string str="";
        answer.push_back(0);
        while(i<msg.length()){
            str+=msg[i];
            if(dict[str]<1) break;  // 못 찾을 경우
            answer.back()=dict[str];
            i++;
        }
        dict[str]=++index;  // 사전 추가
    }

    return answer;
}
```

### JavaScript

```js
function solution(msg) {
  var answer = [];

  // init
  const word = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");
  const dict = new Map(word.map((v, i) => [v, i + 1]));

  for (let i = 0; i < msg.length; ) {
    let str = "";
    answer.push(0);
    while (i < msg.length) {
      str += msg[i];
      if (!dict.has(str)) break; // 못 찾을 경우
      answer[answer.length - 1] = dict.get(str);
      i++;
    }
    dict.set(str, dict.size + 1); // 사전 추가
  }

  return answer;
}
```

---
title: "스킬트리"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-2]
toc: true
toc_sticky: true
---

## 문제 링크

[스킬트리](https://programmers.co.kr/learn/courses/30/lessons/49993)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

int solution(string skill, vector<string> skill_trees) {
    int answer = 0;

    for(string str: skill_trees){
        string s = "";
        for(char ch: str){
            if(skill.find(ch) != string::npos) s += ch;
        }
        if(skill.find(s) == 0) answer++;
    }

    return answer;
}
```

### JavaScript

```js
function solution(skill, skill_trees) {
  var answer = 0;

  skill_trees
    .map((value) => {
      return value
        .split("")
        .filter((value) => {
          return skill.includes(value);
        })
        .join("");
    })
    .some((value) => {
      if (skill.indexOf(value) === 0) answer++;
    });

  return answer;
}
```

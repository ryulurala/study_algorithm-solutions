---
title: "하노이의 탑"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-24"
---

## 문제 링크

[하노이의 탑](https://programmers.co.kr/learn/courses/30/lessons/12946)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

// from --> by --> to
void move(int num, int from, int to, int by, vector<vector<int> >& answer){
    vector<int> v={from, to};
    if(num == 1) answer.push_back(v);   // 1개 남았을 때, push
    else{
        // from --> to --> by
        move(num-1, from, by, to, answer);

        // push
        answer.push_back(v);

        // by --> from --> to
        move(num-1, by, to, from, answer);
    }
}

vector<vector<int>> solution(int n) {
    vector<vector<int>> answer;
    move(n, 1, 3, 2, answer);

    return answer;
}
```

### JavaScript

```js
function solution(n) {
  var answer = [];

  const move = (num, from, to, by) => {
    const sub = [from, to];
    if (num === 1) answer.push(sub);
    // 1개 남았을 경우
    else {
      // from---to---by
      move(num - 1, from, by, to);

      // push
      answer.push(sub);

      // by---from---to
      move(num - 1, by, to, from);
    }
  };

  move(n, 1, 3, 2);

  return answer;
}
```

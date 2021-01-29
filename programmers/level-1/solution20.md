---
title: "수박수박수박수박수박수?"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-20"
---

## 문제 링크

[수박수박수박수박수박수?](https://programmers.co.kr/learn/courses/30/lessons/12922)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

string solution(int n) {
    string answer = "";

    for(int i=0; i<n/2; i++){
        answer += "수박";
    }

    if(n%2!=0) answer += "수";

    return answer;
}
```

### JavaScript

```js
function solution(n) {
  var answer = "";

  for (let i = 0; i < parseInt(n / 2); i++) {
    answer += "수박";
  }

  if (n % 2 != 0) answer += "수";

  return answer;
}
```

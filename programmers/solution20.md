---
title: "수박수박수박수박수박수?"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
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

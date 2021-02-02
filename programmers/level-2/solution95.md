---
title: "n진수 게임"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-03"
---

## 문제 링크

[n진수 게임](https://programmers.co.kr/learn/courses/30/lessons/17687)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

string num2str(int n, int num){
    if(num==0) return "0";

    string LUT="0123456789ABCDEF";
    string ret="";
    while(num>0){
        ret += LUT[num%n];
        num/=n;
    }
    reverse(ret.begin(), ret.end());

    return ret;
}

string solution(int n, int t, int m, int p) {
    string answer = "";

    string total="";
    for(int i=0; ; i++){
        total+=num2str(n, i);   // 나열
        if(total.length()>=m*t) break;
    }

    for(int i=0; i<t; i++){
        answer+=total[(p-1)+m*i];   // 추출
    }

    return answer;
}
```

### JavaScript

```js
function solution(n, t, m, p) {
  var answer = "";

  let total = "";
  for (let i = 0; ; i++) {
    total += i.toString(n); // 나열
    if (total.length >= m * t) break;
  }

  for (let i = 0; i < t; i++) {
    answer += total[p - 1 + m * i]; // 추출
  }
  answer = answer.toUpperCase();

  return answer;
}
```

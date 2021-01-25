---
title: "가장 큰 수"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-25"
---

## 문제 링크

[가장 큰 수](https://programmers.co.kr/learn/courses/30/lessons/42746)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

bool cmp(string a, string b){
    if(a+b<b+a) return true;    // 순서를 바꿔 더해 오름차순
    else return false;
}

string solution(vector<int> numbers) {
    string answer = "";

    vector<string> newNumbers;
    for(int num: numbers){
        newNumbers.push_back(to_string(num));   // string으로 변환
    }

    stable_sort(newNumbers.rbegin(), newNumbers.rend(), cmp);   // 내림차순 형태

    for(string str: newNumbers) answer+=str;

    if(answer[0]=='0') answer='0';

    return answer;
}
```

### JavaScript

```js
function solution(numbers) {
  var answer = "";

  answer = numbers
    .sort((a, b) => {
      if ("" + a + b < "" + b + a) return 1;
      else return -1;
    })
    .join("");

  if (answer[0] === "0") answer = "0";

  return answer;
}
```

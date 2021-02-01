---
title: "뉴스 클러스터링"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-01"
---

## 문제 링크

[뉴스 클러스터링](https://programmers.co.kr/learn/courses/30/lessons/17677)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>
#include <algorithm>

using namespace std;

vector<string> split(string str){
    vector<string> v;

    // 알파벳 소문자로
    for(char& ch: str) ch=tolower(ch);

    // split
    for(int i=1; i<str.length(); i++){
        if(str[i-1]>='a'&&str[i-1]<='z'&&str[i]>='a'&&str[i]<='z'){
            v.push_back(str.substr(i-1, 2));
        }
    }

    return v;
}

int solution(string str1, string str2) {
    int answer = 0;

    // split
    vector<string> v1=split(str1);
    vector<string> v2=split(str2);

    // 정렬 필수
    stable_sort(v1.begin(), v1.end());
    stable_sort(v2.begin(), v2.end());

    vector<string> v3(v1.size()+v2.size());     // 교집합
    auto iter1=set_intersection(v1.begin(), v1.end(), v2.begin(), v2.end(), v3.begin());
    v3.erase(iter1, v3.end());

    vector<string> v4(v1.size()+v2.size());     // 합집합
    auto iter2=set_union(v1.begin(), v1.end(), v2.begin(), v2.end(), v4.begin());
    v4.erase(iter2, v4.end());

    if(v3.empty() && v4.empty()) answer=65536;
    else answer=(float)v3.size()/v4.size()*65536;

    return answer;
}
```

### JavaScript

```js
function solution(str1, str2) {
  var answer = 0;

  const createSet = (str) => {
    const result = [];

    str = str.toLowerCase(); // 일괄적으로 소문자

    for (let i = 1; i < str.length; i++) {
      const tmp = str.slice(i - 1, i + 1);
      if (tmp.match(/[a-z]{2}/)) result.push(tmp);
    }

    return result;
  };

  const arr1 = createSet(str1);
  const arr2 = createSet(str2);

  let union = 0;
  let intersection = 0;
  const totalSet = new Set([...arr1, ...arr2]);

  totalSet.forEach((val) => {
    const has1 = arr1.filter((v) => v === val).length;
    const has2 = arr2.filter((v) => v === val).length;

    union += Math.max(has1, has2);
    intersection += Math.min(has1, has2);
  });

  if (union === 0 && intersection === 0) answer = 65536;
  else answer = parseInt((intersection / union) * 65536);

  return answer;
}
```

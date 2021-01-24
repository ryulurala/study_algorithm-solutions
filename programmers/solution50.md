---
title: "문자열 압축"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-2]
toc: true
toc_sticky: true
---

## 문제 링크

[문자열 압축](https://programmers.co.kr/learn/courses/30/lessons/60057)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

// length/2 개 단위까지

int solution(string s) {
    int answer = 0;

    answer = s.length();
    for(int cut=1; cut<=s.length()/2; cut++){
        vector<string> v;
        for(int i=0; i<s.length(); i+=cut){
            // 문자열 자르기
            v.push_back(s.substr(i, cut));
        }

        string result = "";
        int count = 1;
        for(int i=1; i<v.size(); i++){
            // 문자열 합치기
            if(v[i-1] == v[i]) count++;
            else {
                if(count!=1) result += to_string(count) + v[i-1];
                else result += v[i-1];
                count = 1;
            }
        }
        // 후처리
        if(count!=1) result += to_string(count) + v.back();
        else result += v.back();

        // 최솟값
        answer = min(answer, (int)result.length());
    }

    return answer;
}
```

### JavaScript

```js
function solution(s) {
  var answer = s.length;

  for (let cut = 1; cut <= parseInt(s.length / 2); cut++) {
    const arr = [];
    for (let i = 0; i < s.length; i += cut) {
      // 문자열 자르기
      arr.push(s.substring(i, i + cut));
    }

    let count = 1;
    let str = "";
    for (let i = 1; i < arr.length; i++) {
      // 문자열 합치기
      if (arr[i - 1] == arr[i]) {
        count++;
      } else {
        if (count != 1) str += count + arr[i - 1];
        else str += arr[i - 1];
        count = 1;
      }
    }
    // 후처리
    if (count != 1) str += count + arr[arr.length - 1];
    else str += arr[arr.length - 1];

    answer = Math.min(answer, str.length);
  }

  return answer;
}
```

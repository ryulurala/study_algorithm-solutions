---
title: "비밀지도"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[비밀지도](https://programmers.co.kr/learn/courses/30/lessons/17681)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<string> solution(int n, vector<int> arr1, vector<int> arr2) {
    vector<string> answer;

    for(int i=0; i<n; i++){
        int map = arr1[i] | arr2[i];    // 지도 합치기
        string str = "";
        for(int j=0; j<n; j++){
            str += (map&1) ? '#' : ' ';     // '#' 표시
            map >>= 1;
        }
        reverse(str.begin(), str.end());    // 뒤집기
        answer.push_back(str);
    }

    return answer;
}
```

### JavaScript

```js
function solution(n, arr1, arr2) {
  var answer = [];

  for (let i = 0; i < n; i++) {
    let str = "";
    let map = arr1[i] | arr2[i]; // 지도 합치기
    for (let j = 0; j < n; j++) {
      str += map & 1 ? "#" : " "; // 지도 '#' 표시
      map >>= 1;
    }
    str = str.split("").reverse().join(""); // 뒤집기
    answer.push(str);
  }

  return answer;
}
```

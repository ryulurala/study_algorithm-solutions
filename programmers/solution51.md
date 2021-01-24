---
title: "삼각 달팽이"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-2]
toc: true
toc_sticky: true
---

## 문제 링크

[삼각 달팽이](https://programmers.co.kr/learn/courses/30/lessons/68645)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

vector<int> solution(int n) {
    vector<int> answer;

    vector<vector<int>> vv;
    for(int i=0; i<n; i++){
        // 초기화
        vector<int> v(n, 0);
        vv.push_back(v);
    }

    int option = 0;
    int count = 0;
    int row = -1;    // for. ++row
    int col = 0;
    for(int i=n; i>0; i--){
        if(option%3==0){
            // 내려오기
            for(int j=0; j<i; j++){
                vv[++row][col] = ++count;
            }
        }
        else if(option%3==1){
            // 옆으로 가기
            for(int j=0; j<i; j++){
                vv[row][++col] = ++count;
            }
        }
        else if(option%3==2){
            // 대각선 올라가기
            for(int j=0; j<i; j++){
                vv[--row][--col] = ++count;
            }
        }
        option++;
    }

    // 삼각 달팽이
    for(int i=0; i<n; i++){
        for(int j=0; j<=i; j++){
            answer.push_back(vv[i][j]);
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(n) {
  var answer = [];

  let vec = []; // 저장용
  for (let i = 0; i < n; i++) {
    // 초기화
    vec.push(Array.from({ length: n }, () => 0));
  }

  let option = 0;
  let count = 0;
  let row = -1; // for. ++row
  let col = 0;
  for (let i = n; i > 0; i--) {
    if (option % 3 === 0) {
      // 내려가기
      for (let j = 0; j < i; j++) {
        vec[++row][col] = ++count;
      }
    } else if (option % 3 === 1) {
      // 옆으로 가기(->)
      for (let j = 0; j < i; j++) {
        vec[row][++col] = ++count;
      }
    } else if (option % 3 === 2) {
      // 올라가기
      for (let j = 0; j < i; j++) {
        vec[--row][--col] = ++count;
      }
    }
    option++;
  }

  // 삼각 달팽이
  for (let i = 0; i < n; i++) {
    for (let j = 0; j <= i; j++) {
      answer.push(vec[i][j]);
    }
  }

  return answer;
}
```

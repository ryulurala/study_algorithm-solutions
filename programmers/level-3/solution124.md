---
title: "숫자 게임"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-16"
---

## 문제 링크

[숫자 게임](https://programmers.co.kr/learn/courses/30/lessons/12987)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> A, vector<int> B) {
    int answer = 0;

    // 오름차순 정렬
    stable_sort(A.begin(), A.end());
    stable_sort(B.begin(), B.end());

    int indexA=0;
    int indexB=0;
    while(indexB<B.size()){
        if(A[indexA] < B[indexB++]){
            // B가 이겼을 때
            indexA++;
            answer++;
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(A, B) {
  var answer = 0;

  // 오름차순
  A.sort((a, b) => a - b);
  B.sort((a, b) => a - b);

  let idxA = 0;
  B.forEach((b) => {
    if (A[idxA] < b) {
      // B가 이길 경우
      idxA++;
      answer++;
    }
  });

  return answer;
}
```

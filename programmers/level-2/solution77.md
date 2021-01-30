---
title: "최솟값 만들기"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-31"
---

## 문제 링크

[최솟값 만들기](https://programmers.co.kr/learn/courses/30/lessons/12941)

### C++

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> A, vector<int> B) {
    int answer = 0;

    // 오름차순 정렬
    stable_sort(A.begin(), A.end());
    stable_sort(B.begin(), B.end());

    int left=0;
    int right=A.size()-1;
    while(left<A.size()){
        answer+=(A[left++]*B[right--]);
    }

    return answer;
}
```

### JavaScript

```js
function solution(A, B) {
  var answer = 0;

  // 오름차순 정렬
  A.sort((a, b) => a - b);
  B.sort((a, b) => a - b);

  let left = 0;
  let right = A.length - 1;
  while (left < A.length) {
    answer += A[left++] * B[right--];
  }

  return answer;
}
```

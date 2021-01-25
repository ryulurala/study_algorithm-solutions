---
title: "큰 수 만들기"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-22"
---

## 문제 링크

[큰 수 만들기](https://programmers.co.kr/learn/courses/30/lessons/42883)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

string solution(string number, int k) {
    string answer = "";

    int start=0;
    char maxNum;
    for(int i=0; i<number.length()-k; i++){
        maxNum = number[start];
        for(int j=start; j<=i+k; j++){
            if(maxNum < number[j]){
                maxNum = number[j];
                start = j;
                if(maxNum == '9') break;    // 뒷자리 더 볼 필요 X
            }
        }
        start++;    // 다음 수부터
        answer += maxNum;
    }

    return answer;
}
```

### JavaScript

```js
function solution(number, k) {
  var answer = "";

  let start = 0;
  let maxStr;
  for (let i = 0; i < number.length - k; i++) {
    maxStr = number[start];
    for (let j = start; j <= i + k; j++) {
      if (maxStr < number[j]) {
        maxStr = number[j];
        start = j;
        if (maxStr === "9") break; // 뒷자리 볼 필요 X
      }
    }
    start++; // 다음 수부터
    answer += maxStr;
  }

  return answer;
}
```

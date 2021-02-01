---
title: "소수 만들기"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-01"
---

## 문제 링크

[소수 만들기](https://programmers.co.kr/learn/courses/30/lessons/12977)

### C++

```cpp
#include <vector>
#include <string>
#include <iostream>
#include <algorithm>
#include <cmath>

using namespace std;

int solution(vector<int> nums) {
    int answer = 0;

    string condi(nums.size(), '1');
    condi.replace(0, 3, "000");
    do{
        // 조합
        int sum=0;
        for(int i=0; i<condi.length(); i++){
            if(condi[i]=='0') sum+=nums[i];
        }

        // 소수 판별
        bool isPrime=true;
        for(int i=2; i<=sqrt(sum); i++){
            if(sum%i==0){
                isPrime=false;
                break;
            }
        }
        if(isPrime) answer++;
    }while(next_permutation(condi.begin(), condi.end()));

    return answer;
}
```

### JavaScript

```js
function solution(nums) {
  var answer = 0;

  for (let i = 0; i < nums.length - 2; i++) {
    for (let j = i + 1; j < nums.length - 1; j++) {
      for (let k = j + 1; k < nums.length; k++) {
        // 조합
        const sum = nums[i] + nums[j] + nums[k];

        // 소수 판별
        let isPrime = true;
        for (let m = 2; m <= parseInt(Math.sqrt(sum)); m++) {
          if (sum % m === 0) {
            isPrime = false;
            break;
          }
        }
        if (isPrime) answer++;
      }
    }
  }

  return answer;
}
```

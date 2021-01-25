---
title: "소수 찾기"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-25"
---

## 문제 링크

[소수 찾기](https://programmers.co.kr/learn/courses/30/lessons/42839)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <set>
#include <cmath>

using namespace std;

int solution(string numbers) {
    int answer = 0;

    set<int> nums;

    stable_sort(numbers.begin(), numbers.end());

    do{
        // 완전탐색
        for(int i=1; i<=numbers.length(); i++){
            int num = stoi(numbers.substr(0, i));
            nums.insert(num);   // 중복 제거
        }
    }while(next_permutation(numbers.begin(), numbers.end()));

    for(auto num: nums){
        // 소수 판별
        if(num==0 || num==1) continue;
        bool isPrime=true;
        for(int i=2; i<=sqrt(num); i++){
            if(num%i != 0) continue;
            isPrime=false;
            break;
        }
        if(isPrime) answer++;
    }

    return answer;
}
```

### JavaScript

```js
function solution(numbers) {
  var answer = 0;

  numbers = numbers.split("").sort((a, b) => {
    if (a < b) return -1;
    else return 1;
  });

  let nums = new Set(); // 중복 제거
  let visit = Array.from({ length: numbers.length }, () => 0);
  const dfsGo = (level, num) => {
    if (level === numbers.length) {
      for (let i = 0; i < num.length; i++) {
        nums.add(+num.substring(i)); // 정수로 push
      }
      return;
    }

    for (let i = 0; i < numbers.length; i++) {
      if (visit[i]) continue;
      num += numbers[i];

      visit[i] = 1;
      dfsGo(level + 1, num);
      num = num.slice(0, num.length - 1);
      visit[i] = 0;
    }
  };
  dfsGo(0, "");

  for (let num of nums) {
    if (num === 0 || num === 1) continue;
    let isPrime = true;
    for (let i = 2; i <= Math.sqrt(num); i++) {
      if (num % i !== 0) continue;
      isPrime = false;
      break;
    }
    if (isPrime) answer++;
  }

  return answer;
}
```

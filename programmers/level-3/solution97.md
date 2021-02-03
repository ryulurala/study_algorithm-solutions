---
title: "N으로 표현"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-03"
---

## 문제 링크

[N으로 표현](https://programmers.co.kr/learn/courses/30/lessons/42895)

### C++

```cpp
#include <string>
#include <vector>
#include <set>

using namespace std;

int solution(int N, int number) {
    int answer = -1;

    // DP
    set<int> nums[8];
    int num=0;
    for(int i=0; i<8; i++){
        // init
        num=num*10+N;   // 5, 55, 555
        nums[i].insert(num);
        for(int j=0; j<i; j++){
            for(int num1: nums[j]){
                for(int num2: nums[i-j-1]){ // i-(j+1)
                    nums[i].insert(num1+num2);  // '+'
                    nums[i].insert(num1-num2);  // '-'
                    nums[i].insert(num1*num2);  // '*'
                    if(num2!=0) nums[i].insert(num1/num2);  // '/'
                }
            }
        }
        if(nums[i].count(number)){
            // number가 있을 경우
            answer=i+1;
            break;
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(N, number) {
  var answer = -1;

  // DP
  const nums = [];
  let num = 0;
  for (let i = 0; i < 8; i++) {
    num = num * 10 + N; // 5, 55, 555
    const set = new Set([num]);
    nums.push(set);
    for (let j = 0; j < i; j++) {
      for (const num1 of nums[j]) {
        for (const num2 of nums[i - j - 1]) {
          // i-(j+1)
          nums[i].add(num1 + num2); // '+'
          nums[i].add(num1 - num2); // '-'
          nums[i].add(num1 * num2); // '*'
          if (num2 !== 0) nums[i].add(num1 / num2); // '/'
        }
      }
    }
    if (nums[i].has(number)) {
      // number가 있을 경우
      answer = i + 1;
      break;
    }
  }

  return answer;
}
```

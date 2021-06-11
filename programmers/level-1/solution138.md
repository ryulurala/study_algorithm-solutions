---
title: "로또의 최고 순위와 최저 순위"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-06-11"
---

## 문제 링크

[로또의 최고 순위와 최저 순위](https://programmers.co.kr/learn/courses/30/lessons/77484)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> lottos, vector<int> win_nums) {
    vector<int> answer;

    // 낙첨, 낙첨, 5등, 4등, ..., 1등
    int lookup[] = {6, 6, 5, 4, 3, 2 ,1};

    // 낙서한 갯수
    int zeroCount = 0;
    for(int e: lottos){
        if(e == 0) zeroCount++;
    }

    // 맞은 갯수
    int winCount = 0;
    for(int winNum: win_nums){
        for(int have: lottos){
            if(have != winNum) continue;

            winCount++;
            break;
        }
    }

    // 최대, 최소
    answer.push_back(lookup[winCount+zeroCount]);
    answer.push_back(lookup[winCount]);

    return answer;
}
```

### JavaScript

```js
function solution(lottos, win_nums) {
  var answer = [];

  // 낙첨, 낙첨, 5등, 4등, ..., 1등
  const lookup = [6, 6, 5, 4, 3, 2, 1];

  // 알아볼 수 없는 숫자 갯수
  const zeroCount = lottos.reduce((prev, value) => {
    if (value === 0) prev++;

    return prev;
  }, 0);

  // 맞춘 갯수
  const winCount = win_nums.reduce((prev, value) => {
    for (const have of lottos) {
      if (have === value) {
        prev++;
        break;
      }
    }

    return prev;
  }, 0);

  // 최대, 최소
  answer.push(lookup[winCount + zeroCount]);
  answer.push(lookup[winCount]);

  return answer; // 최고 순위, 최저 순위
}
```

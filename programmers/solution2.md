---
title: "두 개 뽑아서 더하기"
excerpt: "프로그래머스 풀이"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
toc: true
toc_sticky: true
---

## 문제 링크

[두 개 뽑아서 더하기](https://programmers.co.kr/learn/courses/30/lessons/68644)

### C++

```cpp
#include <string>
#include <vector>
#include <set>

using namespace std;

vector<int> solution(vector<int> numbers) {
    vector<int> answer;
    set<int> _set;      // 중복 제거, 오름차순 자동 정렬

    for(int i=0; i<numbers.size(); i++){
        for(int j=i+1; j<numbers.size(); j++){
            _set.insert(numbers[i] + numbers[j]);   // push
        }
    }

    for(auto e: _set){
        answer.push_back(e);    // copy
    }

    return answer;
}
```

### JavaScript

```js
function solution(numbers) {
  var answer = [];

  for (let i = 0; i < numbers.length; i++) {
    for (let j = i + 1; j < numbers.length; j++) {
      let sum = numbers[i] + numbers[j];
      if (answer.includes(sum)) continue;
      answer.push(sum); // 중복이 아닐경우
    }
  }

  answer.sort((a, b) => {
    return a - b; // 오름차순 정렬
  });

  return answer;
}
```

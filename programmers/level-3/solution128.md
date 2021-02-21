---
title: "스타 수열"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-21"
---

## 문제 링크

[스타 수열](https://programmers.co.kr/learn/courses/30/lessons/70130)

### C++

```cpp
#include <string>
#include <vector>
#include <map>
#include <iostream>

using namespace std;

int solution(vector<int> a) {
    int answer = 0;

    map<int, int> num_count;
    for(int e: a) num_count[e]++;   // 중복 숫자 갯수

    for(auto p: num_count){
        if(p.second<answer/2) continue;   // 스타수열 길이 이미 짧음
        int select=p.first;

        int starLen=0;
        for(int i=1; i<a.size(); i++){
            if(a[i-1]!=select && a[i]!=select) continue;    // 선택한 수랑 다를 경우
            else if(a[i-1]==a[i]) continue;     // 연속 X

            // 스타 수열
            starLen+=2;
            i++;    // for. 2칸 next
        }

        answer=max(answer, starLen);    // 최대 갱신
    }

    return answer;
}
```

### JavaScript

```js
function solution(a) {
  var answer = 0;

  // 중복 숫자 개수 세기
  const num_count = new Map();
  a.forEach((v) => {
    if (num_count.has(v)) {
      num_count.set(v, num_count.get(v) + 1);
    } else {
      num_count.set(v, 1);
    }
  });

  for (const [select, count] of num_count) {
    if (count < answer) continue; // 이미 스타 수열 길이 작음

    let cnt = 0;
    for (let i = 1; i < a.length; i++) {
      if (a[i - 1] !== select && a[i] !== select) continue;
      // 지정된 숫자랑 둘다 다를 경우
      else if (a[i - 1] === a[i]) continue; // 연속으로 같을 경우

      // 스타 수열 가능
      cnt++;
      i++; // for. 2칸 next
    }
    answer = Math.max(answer, cnt);
  }

  return answer * 2;
}
```

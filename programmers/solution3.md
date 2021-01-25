---
title: "완주하지 못한 선수"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-18"
---

## 문제 링크

[완주하지 못한 선수](https://programmers.co.kr/learn/courses/30/lessons/42576)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

string solution(vector<string> participant, vector<string> completion) {
    string answer = "";
    sort(participant.begin(), participant.end());   // 정렬
    sort(completion.begin(), completion.end());     // 정렬

    int i=0;
    while(true){
        if(participant[i] != completion[i]) break;  // 완주한 이름과 다르면
        i++;
    }

    answer = participant[i];    // 완주하지 못한 사람

    return answer;
}
```

### JavaScript

```js
function solution(participant, completion) {
  var answer = "";
  participant.sort((person1, person2) => {
    // person2가 더 크거나 같으면 안 바꿈(오름차순: 사전 정렬)
    return person1 < person2 ? 1 : person1 === person2 ? 0 : -1;
  });
  completion.sort((person1, person2) => {
    // 사전 정렬
    return person1 < person2 ? 1 : person1 === person2 ? 0 : -1;
  });

  let i = 0;
  while (true) {
    if (participant[i] !== completion[i]) break; // 완주한 선수와 다르면
    i++;
  }
  answer = participant[i]; // 완주하지 못한 사람

  return answer;
}
```

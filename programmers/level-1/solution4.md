---
title: "모의고사"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-18"
---

## 문제 링크

[모의고사](https://programmers.co.kr/learn/courses/30/lessons/42840)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(vector<int> answers) {
    vector<int> answer;
    vector<int> scores(3, 0);    // 3개 공간을 모두 0으로 초기화

    string person1 = "12345";       // 1번 수포자
    string person2 = "21232425";    // 2번 수포자
    string person3 = "3311224455";  // 3번 수포자

    for(int i=0; i<answers.size(); i++){
        int answer = answers[i] + '0';  // char 변환
        if(person1[i%5] == answer) scores[0]++;     // 1번 수포자 맞춤
        if(person2[i%8] == answer) scores[1]++;     // 2번 수포자 맞춤
        if(person3[i%10] == answer) scores[2]++;    // 3번 수포자 맞춤
    }

    // 가장 많이 맞춘 점수
    int maxScore = *max_element(scores.begin(), scores.end());

    for(int i=0; i<scores.size(); i++){
        if(maxScore === scores[i])
            answer.push_back(i+1);    // 가장 많이 맞춘 사람
    }

    return answer;
}
```

### JavaScript

```js
function solution(answers) {
  var answer = [];

  let scores = [0, 0, 0];
  let person1 = "12345"; // 1번 수포자
  let person2 = "21232425"; // 2번 수포자
  let person3 = "3311224455"; // 3번 수포자

  for (let i = 0; i < answers.length; i++) {
    // 일부러 타입 비교 유연
    if (person1[i % 5] == answers[i]) scores[0]++; // 1번 수포자 정답
    if (person2[i % 8] == answers[i]) scores[1]++; // 2번 수포자 정답
    if (person3[i % 10] == answers[i]) scores[2]++; // 3번 수포자 정답
  }

  let maxScore = Math.max.apply(null, scores); // 점수 최댓값
  for (let i = 0; i < answers.length; i++) {
    if (maxScore === scores[i]) answer.push(i + 1); // 가장 많이 맞춘 수포자
  }

  return answer;
}
```

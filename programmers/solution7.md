---
title: "2016년"
excerpt: "프로그래머스 풀이"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
toc: true
toc_sticky: true
---

## 문제 링크

[2016년](https://programmers.co.kr/learn/courses/30/lessons/12901)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

// 윤년: 366일

string solution(int a, int b) {
    string answer = "";
    string days[7] = {"SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT"};
    int month[12] = {31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

    int day = -1;    // 처음은 1일 이므로 하루 빼기
    for(int i=0; i<a-1; i++){
        day += month[i];    // '월'마다 '일' 수 더하기
    }
    day += b;   // '일' 수 더하기
    answer = days[(5+day) % 7];

    return answer;
}
```

### JavaScript

```js
function solution(a, b) {
  var answer = "";

  let days = ["SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT"];
  let month = [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];

  let day = -1; // 처음이 1일이므로 하루 빼기
  for (let i = 0; i < a - 1; i++) {
    day += month[i]; // 달마다 일 수 더하기
  }
  day += b; // 해당 일 수 더하기

  answer = days[(5 + day) % 7]; // 요일 구하기, 처음은 금요일

  return answer;
}
```

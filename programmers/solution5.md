---
title: "체육복"
excerpt: "프로그래머스 풀이"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
toc: true
toc_sticky: true
---

## 문제 링크

[체육복](https://programmers.co.kr/learn/courses/30/lessons/42862)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

// n 전체 학생 수
// lost 도난당한 학생들의 번호가 담긴 배열
// reserve 여별의 체육복을 가져온 학생들의 번호가 담긴 배열

int solution(int n, vector<int> lost, vector<int> reserve) {
    int answer = 0;

    // 모든 학생이 체육복 가져옴
    // 맨 처음과 끝 무조건 체육복 존재(에러 처리)
    vector<int> students(n+2, 1);

    for(auto e: lost) students[e]--;     // 체육복 도난당함
    for(auto e: reserve) students[e]++;  // 여벌 체육복이 존재

    for(int i=1; i<students.size(); i++){
        if(students[i]==2){
            if(students[i-1]==0){
                // 앞에 사람에게 빌려줌
                students[i]--;
                students[i-1]++;
            } else if(students[i+1]==0){
                // 뒤에 사람에게 빌려줌
                students[i]--;
                students[i+1]++;
            }
        }
    }

    for(auto e: students){
        if(e > 0) answer++;
    }

    return answer-2;      // 체육 수업을 들을 수 있는 학생 수 최댓값
}
```

### JavaScript

```js
function solution(n, lost, reserve) {
  var answer = 0;

  // 모든 학생들은 체육복을 가지고 있다.
  // n+2: error 처리
  let students = Array.from({ length: n + 2 }, (v, i) => 1);

  lost.forEach((item) => {
    students[item]--; // 체육복 도난당함
  });
  reserve.forEach((item) => {
    students[item]++; // 여벌 체육복 보유
  });

  students.forEach((item, index, array) => {
    if (item == 2) {
      if (array[index - 1] == 0) {
        array[index]--; // 빌려줌
        array[index - 1]++; // 체육복 생김
      } else if (students[index + 1] == 0) {
        array[index]--; // 빌려줌
        array[index + 1]++; // 체육복 생김
      }
    }
  });

  students.forEach((item) => {
    if (item > 0) answer++; // 체육복 있는 학생 수
  });

  return answer - 2; // 처음과 끝 제외
}
```

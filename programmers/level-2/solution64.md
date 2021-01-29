---
title: "구명보트"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-28"
---

## 문제 링크

[구명보트](https://programmers.co.kr/learn/courses/30/lessons/42885)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> people, int limit) {
    int answer = 0;

    stable_sort(people.begin(), people.end());  // 오름차순 정렬

    int weight=0;   // 현재 무게
    int front=0;
    int back=people.size()-1;
    while(front<=back){
        if(front<back) weight=people[front]+people[back];
        else weight=people[front];
        answer++; // 구명 보트 1개 추가

        back--;  // 뒤에 사람은 무조건 pop
        if(front>back) break;   // 모두 구조했을 경우

        if(weight<=limit) front++; // 가능할 때 pop
        weight=0;
    }

    return answer;
}
```

### JavaScript

```js
function solution(people, limit) {
  var answer = 0;

  people.sort((a, b) => a - b);

  let front = 0;
  let back = people.length - 1;
  let weight = 0;
  while (front <= back) {
    if (front != back) weight = people[front] + people[back];
    else weight = people[back];
    answer++; // 구명보트 1개 추가

    back--; // 뒷 사람은 무조건 pop
    if (front > back) break;

    if (weight <= limit) front++; // 앞 사람은 가능할 때만
    weight = 0; // 무게 초기화
  }

  return answer;
}
```

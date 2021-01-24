---
title: "다리를 지나는 트럭"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-2]
toc: true
toc_sticky: true
---

## 문제 링크

[다리를 지나는 트럭](https://programmers.co.kr/learn/courses/30/lessons/42583)

### C++

```cpp
#include <string>
#include <vector>
#include <queue>

using namespace std;

int solution(int bridge_length, int weight, vector<int> truck_weights) {
    int answer = 0;

    queue<int> q;
    int sum = 0;
    for(auto truck: truck_weights){
        while(sum > 0){
            // 트럭이 다리에 있는 경우
            if(q.size() == bridge_length){
                // 트럭이 다리를 지나감
                sum -= q.front();
                q.pop();
            }
            if(sum+truck > weight){
                // 트럭을 못올림
                q.push(0);
                answer++;
            }
            else{
                // 트럭을 올린다
                q.push(truck);
                sum += truck;
                answer++;
                break;
            }
        }
        if(q.empty()){
            sum += truck;
            q.push(truck);
            answer++;
        }
    }
    answer += bridge_length;    // 마지막 트럭이 다리에 들어오고 반복분 종료

    return answer;
}
```

### JavaScript

```js
function solution(bridge_length, weight, truck_weights) {
  var answer = 0;

  const queue = [];
  let sum = 0;
  truck_weights.some((truck) => {
    if (queue.length > 0) {
      while (true) {
        if (queue.length === bridge_length) {
          // 트럭이 다리를 지나감
          sum -= queue.shift();
        }
        if (sum + truck <= weight) {
          // 트럭을 올림
          queue.push(truck);
          sum += truck;
          answer++;
          break;
        } else {
          // 길이만 늘림
          queue.push(0);
          answer++;
        }
      }
    } else {
      sum += truck;
      queue.push(truck);
      answer++;
    }
  });
  answer += bridge_length; // 다리에 대기 트럭이 올라간 시점이므로

  return answer;
}
```

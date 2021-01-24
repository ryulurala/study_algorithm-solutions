---
title: "징검다리 건너기"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-3]
toc: true
toc_sticky: true
---

## 문제 링크

[징검다리 건너기](https://programmers.co.kr/learn/courses/30/lessons/64062)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> stones, int k) {
    int answer = 0;

    int right=*max_element(stones.begin(), stones.end());   // 최대 인원
    int left=1;     // 한 명이상

    while(left<=right){
        int mid=(left+right)/2;     // 중간값
        int count=0;
        for(int i=0; i<stones.size(); i++){
            if(stones[i]<mid){
                count++;    // 연속됨
                if(count>=k) { count=-1; break;}
            }
            else count=0;
        }
        if(count<0){
            // 실패
            right=mid-1;
        }
        else{
            // 성공
            left=mid+1;
            answer=mid;
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(stones, k) {
  var answer = 0;

  let left = 1; // 한 명부터
  // let right=Math.max(...stones);  // 런타임에러
  let right = 200000000; // 최대 인원

  while (left <= right) {
    const mid = parseInt((left + right) / 2);
    let count = 0;
    stones.some((stone) => {
      if (stone < mid) {
        count++; // 연속됨
        if (count == k) {
          count = -1;
          return true;
        }
      } else count = 0;
    });
    if (count === -1) {
      // 실패
      right = mid - 1;
    } else {
      // 성공
      left = mid + 1;
      answer = mid; // 최솟값 갱신
    }
  }

  return answer;
}
```

---
title: "외벽 점검"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-14"
---

## 문제 링크

[외벽 점검](https://programmers.co.kr/learn/courses/30/lessons/60062)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(int n, vector<int> weak, vector<int> dist) {
    int answer = 9;     // 최대

    sort(dist.begin(), dist.end());  // for. next_permutation()

    for(int i=0; i<weak.size(); i++){
        // 완전탐색, 취약위치 시작지점마다
        do{
            // 완전탐색, dist 순서 바꿔가면서
            int w=0;    // weak 인덱스

            for(int d=0; d<dist.size(); d++){
                int after=weak[w]+dist[d];  // 취약위치 지점에서 시작한 1시간 후 지점

                while(w<weak.size()){
                    if(after<weak[w]) break;    // 취약위치에 도달 못함
                    w++;
                }

                if(w==weak.size()){
                    // 취약 지점 모두 해결
                    answer=min(answer, d+1);
                    break;
                }
            }
        }while(next_permutation(dist.begin(), dist.end()));

        weak.push_back(weak.front()+n);     // 직선화
        weak.erase(weak.begin());   // 앞에꺼 삭제
    }
    answer=answer==9?-1:answer;     // 취약지점 해결 불가

    return answer;
}
```

### JavaScript

```js
function solution(n, weak, dist) {
  var answer = 9; // 최대

  const getPermu = (arr, select) => {
    if (select === 1) return arr.map((v) => [v]);
    else {
      const result = [];
      arr.forEach((val, idx) => {
        const fixed = val; // 1개 선택
        const restArr = arr.filter((v, i) => idx !== i); // 나머지 배열
        const permuArr = getPermu(restArr, select - 1); // 재귀
        const mergeArr = permuArr.map((v) => [fixed, ...v]); // 합치기
        result.push(...mergeArr);
      });
      return result;
    }
  };
  const distPermu = getPermu(dist, dist.length); // 순열
  for (let i = 0; i < weak.length; i++) {
    // weak 시작지점마다
    distPermu.forEach((newDist) => {
      // dist 순서 변경한 newDist마다
      let w = 0; // weak index

      for (let d = 0; d < newDist.length; d++) {
        const after = weak[w] + newDist[d]; // 취약지점부터 1시간 후 지점

        while (w < weak.length) {
          if (after < weak[w]) break; // 취약지점 해결 못함
          w++;
        }

        // 취약지점 모두 해결
        if (w === weak.length) {
          answer = Math.min(answer, d + 1);
          break;
        }
      }
    });

    weak.push(weak[0] + n); // 직선화
    weak.shift(); // 앞에꺼 제거
  }
  answer = answer === 9 ? -1 : answer; // 해결 못함

  return answer;
}
```

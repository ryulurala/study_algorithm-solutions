---
title: "다음 큰 숫자"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-30"
---

## 문제 링크

[다음 큰 숫자](https://programmers.co.kr/learn/courses/30/lessons/12911)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

int countOfOne(int num){    // 1의 개수 세는 함수
    int cnt=0;
    while(num>0){
        if(num&1) cnt++;
        num>>=1;  // 자연수니까 MSB는 0
    }
    return cnt;
}

int solution(int n) {
    int answer = 0;

    int countN=countOfOne(n);
    for(int i=n+1; i<1000000; i++){
        if(countN==countOfOne(i)){
            answer=i;
            break;
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(n) {
  var answer = 0;

  // 1의 개수 세는 함수
  const countOfOne = (num) => {
    let cnt = 0;
    num
      .toString(2)
      .split("")
      .forEach((val, idx) => {
        if (+val === 1) cnt++;
      });
    return cnt;
  };

  const countN = countOfOne(n);
  for (let i = n + 1; i <= 1000000; i++) {
    if (countOfOne(i) === countN) {
      answer = i;
      break;
    }
  }

  return answer;
}
```

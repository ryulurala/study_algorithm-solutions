---
title: "약수의 합"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[약수의 합](https://programmers.co.kr/learn/courses/30/lessons/12928)

### C++

```cpp
#include <string>
#include <vector>
#include <cmath>

using namespace std;

int solution(int n) {
    int answer = 0;

    for(int i=1; i<=sqrt(n); i++){
        if(n % i == 0){
            answer += i;
            if(i*i != n) answer += n/i;
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(n) {
  var answer = 0;

  for (let i = 1; i <= parseInt(Math.sqrt(n)); i++) {
    if (n % i === 0) {
      answer += i;
      if (i * i != n) answer += parseInt(n / i);
    }
  }

  return answer;
}
```

---
title: "K번째수"
excerpt: "프로그래머스 풀이"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
toc: true
toc_sticky: true
---

## 문제 링크

[K번째 수](https://programmers.co.kr/learn/courses/30/lessons/42748)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(vector<int> array, vector<vector<int>> commands) {
    vector<int> answer;

    for(auto item: commands){
        vector<int> _vec;
        for(int i=item[0]-1; i<item[1]; i++){
            _vec.push_back(array[i]);       // 새로운 배열
        }
        stable_sort(_vec.begin(), _vec.end());  // 오름차순 정렬
        answer.push_back(_vec[item[2]-1]);      // 숫자 추출
    }

    return answer;
}
```

### JavaScript

```js
function solution(array, commands) {
  var answer = [];

  commands.forEach((item) => {
    let newArray = array.slice(item[0] - 1, item[1]); // 부분 배열
    newArray.sort((a, b) => {
      // 오름차순 정렬
      return a < b ? -1 : a === b ? 0 : 1;
    });
    console.log(newArray);
    answer.push(newArray[item[2] - 1]); // 결과 담기
  });

  return answer;
}
```

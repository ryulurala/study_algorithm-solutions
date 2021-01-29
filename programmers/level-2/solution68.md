---
title: "쿼드압축 후 개수 세기"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-29"
---

## 문제 링크

[쿼드압축 후 개수 세기](https://programmers.co.kr/learn/courses/30/lessons/68936)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

int countZero, countOne;  // 각각 0과 1의 개수

void divideGo(vector<vector<int>>& arr, int row, int col, int size){
    int count=0;

    for(int x=row; x<row+size; x++){
        for(int y=col; y<col+size; y++){
            count+=arr[x][y];
        }
    }

    if(count==size*size) countOne++;    // 1로 압축
    else if(count==0) countZero++;      // 0으로 압축
    else{
        divideGo(arr, row, col, size/2);
        divideGo(arr, row, col+size/2, size/2);
        divideGo(arr, row+size/2, col, size/2);
        divideGo(arr, row+size/2, col+size/2, size/2);
    }
}

vector<int> solution(vector<vector<int>> arr) {
    vector<int> answer;

    countZero=countOne=0;

    divideGo(arr, 0, 0, arr.size());

    answer.push_back(countZero);
    answer.push_back(countOne);

    return answer;
}
```

### JavaScript

```js
function solution(arr) {
  var answer = [];

  let countZero = 0; // 0 개수
  let countOne = 0; // 1 개수

  const divideGo = (row, col, size) => {
    let cnt = 0;

    for (let x = row; x < row + size; x++) {
      for (let y = col; y < col + size; y++) {
        cnt += arr[x][y];
      }
    }

    if (cnt === 0) countZero++;
    // 0으로 압축
    else if (cnt === size * size) countOne++;
    // 1로 압축
    else {
      divideGo(row, col, size / 2); // 좌상
      divideGo(row, col + size / 2, size / 2); // 우상
      divideGo(row + size / 2, col, size / 2); // 좌하
      divideGo(row + size / 2, col + size / 2, size / 2); // 우하
    }
  };

  divideGo(0, 0, arr.length);

  answer.push(countZero);
  answer.push(countOne);

  return answer;
}
```

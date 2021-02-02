---
title: "후보키"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-03"
---

## 문제 링크

[후보키](https://programmers.co.kr/learn/courses/30/lessons/42890)

### C++

```cpp
#include <string>
#include <vector>
#include <set>

using namespace std;

int solution(vector<vector<string>> relation) {
    int answer = 0;

    int row=relation.size();
    int col=relation[0].size();
    vector<int> cKeys;
    for(int k=1; k<(1<<col); k++){
        // 최소성 판별
        bool isMinimal=true;
        for(int key: cKeys){
            if((key&k)==key){
                isMinimal=false;
                break;
            }
        }
        if(!isMinimal) continue;    // 최소성 불가

        // 유일성 판별
        set<string> values;
        for(int i=0; i<row; i++){
            string value="";
            for(int j=0; j<col; j++){
                if(k&(1<<j)) value+=relation[i][j];
            }
            values.insert(value);
        }
        if(values.size()!=row) continue;    // 유일성 불가

        cKeys.push_back(k);     // 후보키 인덱스 push
    }
    answer=cKeys.size();

    return answer;
}
```

### JavaScript

```js
function solution(relation) {
  var answer = 0;

  const row = relation.length;
  const col = relation[0].length;
  const cKeys = [];
  for (let k = 1; k < 1 << col; k++) {
    // 최소성 판별
    let isMinimal = true;
    for (const key of cKeys) {
      if ((key & k) === key) {
        isMinimal = false;
        break;
      }
    }
    if (!isMinimal) continue; // 최소성 불가

    // 유일성 판별
    const set = new Set();
    for (let i = 0; i < row; i++) {
      let value = "";
      for (let j = 0; j < col; j++) {
        if (k & (1 << j)) value += relation[i][j];
      }
      set.add(value);
    }
    if (set.size !== row) continue; // 유일성 불가

    cKeys.push(k); // 후보키 push
  }
  answer = cKeys.length;

  return answer;
}
```

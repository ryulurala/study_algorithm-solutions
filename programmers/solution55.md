---
title: "튜플"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-2]
toc: true
toc_sticky: true
---

## 문제 링크

[튜플](https://programmers.co.kr/learn/courses/30/lessons/64065)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

bool cmp(vector<int> a, vector<int> b){
    return a.size() < b.size();
}

vector<int> solution(string s) {
    vector<int> answer;

    s.erase(s.begin());     // '{' 제거
    s.pop_back();       // '}' 제거

    vector<vector<int>> tuples;
    vector<int> v;
    string str="";
    for(char ch: s){
        // split
        if(ch>='0'&&ch<='9') str+=ch;
        else if(ch==','&&!str.empty()){
            v.push_back(stoi(str));
            str="";
        }
        else if(ch=='}'){
            v.push_back(stoi(str));
            str="";
            vector<int> temp;
            swap(v, temp);
            tuples.push_back(temp);
        }
    }

    sort(tuples.begin(), tuples.end(), cmp);    // length로 정렬

    int prev = tuples[0][0];
    answer.push_back(prev);
    for(int i=1; i<tuples.size(); i++){
        int curr = 0;
        for(int num: tuples[i]){
            curr += num;
        }
        answer.push_back(curr-prev);    // 현재 합-이전 합
        prev = curr;
    }

    return answer;
}
```

### JavaScript

```js
function solution(s) {
  var answer = [];

  JSON.parse(s.replace(/[{]/g, "[").replace(/[}]/g, "]")) // array 파싱
    .sort((a, b) => {
      return a.length - b.length; // length로 정렬
    })
    .reduce((prev, value) => {
      let sum = 0;
      for (const i in value) {
        sum += value[i];
      }
      answer.push(sum - prev); // 합 차이로 push
      return sum;
    }, 0);

  return answer;
}
```

---
title: "순위 검색"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-29"
---

## 문제 링크

[순위 검색](https://programmers.co.kr/learn/courses/30/lessons/72412)

### C++

```cpp
#include <string>
#include <vector>
#include <map>
#include <algorithm>
#include <sstream>

using namespace std;

vector<int> solution(vector<string> info, vector<string> query) {
    vector<int> answer;

    map<string, vector<int>> info_score;    // 조건(key)_점수(value)

    for(string& str: info){
        // split
        vector<string> v(4);
        stringstream ss(str);
        for(int i=0; i<4; i++){
            ss >> v[i];
        }
        int score;
        ss >> score;

        // 조합(모든 경우의 수)
        for(int i=0; i<=4; i++){
            string s1(i, '0');
            string s2(4-i, '1');
            string condi=s1+s2;
            do{
                string s3="";
                for(int j=0; j<4; j++){
                    if(condi[j]=='0') s3+=v[j];
                    else s3+='-';
                }
                info_score[s3].push_back(score);

            }while(next_permutation(condi.begin(), condi.end()));
        }
    }

    // 점수 오름차순 정렬
    for(auto& e: info_score){
        stable_sort(e.second.begin(), e.second.end());
    }

    // Query
    for(string& str: query){
        int score;
        string key="";

        stringstream ss(str);

        // 파싱
        for(int i=0; i<7; i++){
            string tempStr;
            ss >> tempStr;
            if(!(i&1)) key+=tempStr;
        }
        ss >> score;

        vector<int> scores=info_score[key];

        // 이진 탐색
        int index=lower_bound(scores.begin(), scores.end(), score) - scores.begin();

        answer.push_back(scores.size()-index);
    }

    return answer;
}
```

### JavaScript

```js
function solution(info, query) {
  var answer = [];

  // 조합 함수
  const combi = (arr, selectNum) => {
    const result = [];
    if (selectNum === 1) return arr.map((v) => [v]);
    else {
      arr.forEach((val, idx) => {
        const fixed = val;
        const restArr = arr.slice(idx + 1);
        const combiArr = combi(restArr, selectNum - 1);
        const mergeArr = combiArr.map((v) => [fixed, ...v]);
        result.push(...mergeArr);
      });
      return result;
    }
  };

  // 이분탐색 함수
  const bsGo = (arr, tgt) => {
    let left = 0;
    let right = arr.length;
    while (left < right) {
      const mid = parseInt((left + right) / 2);

      if (arr[mid] < tgt) {
        left = mid + 1;
      } else {
        right = mid;
      }
    }
    return left;
  };

  const info_score = new Map();
  info_score.set("", []); // 모든 경우

  // info 파싱
  info.forEach((val) => {
    val = val.split(" ");
    const score = val[val.length - 1];
    val.pop();
    info_score.get("").push(+score); // 모든 경우

    // 조합(모든 경우의 수)
    for (let i = 1; i <= 4; i++) {
      const comb = combi("0123".split(""), i);
      comb.forEach((index) => {
        const key = index.map((v) => val[+v]).join("");
        if (info_score.has(key)) {
          info_score.get(key).push(+score);
        } else {
          info_score.set(key, [+score]);
        }
      });
    }
  });
  for (const [key, value] of info_score) {
    value.sort((a, b) => a - b); // 오름차순 정렬
  }

  // 쿼리 파싱
  query.forEach((val) => {
    val = val.replace(/\sand\s|\-/gi, "").split(" ");
    const key = val[0];
    const score = +val[1];
    if (info_score.has(key)) {
      // 해당 key가 있을 경우
      const scores = info_score.get(key);

      // 이분탐색
      const index = bsGo(scores, score);
      answer.push(scores.length - index);
    } else {
      // 해당 key 존재 X
      answer.push(0);
    }
  });

  return answer;
}
```

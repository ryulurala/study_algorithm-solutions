---
title: "불량 사용자"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-3]
toc: true
toc_sticky: true
---

## 문제 링크

[불량 사용자](https://programmers.co.kr/learn/courses/30/lessons/64064)

### C++

```cpp
#include <string>
#include <vector>
#include <set>
#include <iostream>

using namespace std;

int bIdLength;
set<set<string>> list;

bool isEqual(string uId, string bId){   // 제제 Id 체크
    if(uId.length() != bId.length()) return false;
    for(int i=0; i<uId.length(); i++){
        if(bId[i]=='*') continue;
        else if(uId[i]==bId[i]) continue;
        return false;
    }
    return true;
}

void dfsGo(int level, vector<vector<string>>& lookup, set<string>& currentSet){
    if(level == bIdLength) {
        list.insert(currentSet);
        return;
    }

    for(int i=0; i<lookup[level].size(); i++){
        string bId = lookup[level][i];
        if(currentSet.count(bId)==1) continue;  // 이미 있으면 Skip
        currentSet.insert(bId); // 넣기
        dfsGo(level+1, lookup, currentSet);     // dfs level 올리기
        currentSet.erase(currentSet.find(bId)); // 지워주기
    }
    return;
}

int solution(vector<string> user_id, vector<string> banned_id) {
    int answer = 0;
    bIdLength = banned_id.size();

    vector<vector<string>> vv;  // banned_id 경우의 수

    for(string bId: banned_id){
        vector<string> v;
        for(string uId: user_id){
            if(isEqual(uId, bId)) v.push_back(uId);
        }
        vv.push_back(v);
    }

    set<string> cs;
    dfsGo(0, vv, cs);

    answer = list.size();

    return answer;
}
```

### JavaScript

```js
function solution(user_id, banned_id) {
  var answer = 0;

  const isEqual = (bId, uId) => {
    // id 체크 함수
    if (bId.length !== uId.length) {
      return false;
    } else {
      for (let i = 0; i < bId.length; i++) {
        if (bId[i] === "*") continue;
        else if (bId[i] === uId[i]) continue;
        return false;
      }
      return true;
    }
  };

  const bIdList = banned_id.map((bId) => {
    // dfs 돌릴 리스트 목록 추출
    let arr = [];
    for (const uId of user_id) {
      if (isEqual(bId, uId)) arr.push(uId);
    }
    return arr;
  });

  let globalSet = new Set(); // 중복 제거
  let currSet = [];

  const dfsGo = (level) => {
    if (level === banned_id.length) {
      const str = currSet.sort().join(""); // 중복 제거
      globalSet.add(str);
      return;
    } else {
      for (const bId of bIdList[level]) {
        if (currSet.includes(bId)) continue;
        currSet.push(bId);
        dfsGo(level + 1);
        currSet.splice(currSet.indexOf(bId), 1);
      }
      return;
    }
  };
  dfsGo(0);

  answer = globalSet.size;

  return answer;
}
```

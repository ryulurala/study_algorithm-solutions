---
title: "회의실 배정(1931)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-05-20"
---

## 문제 링크

[회의실 배정(1931)](https://www.acmicpc.net/problem/1931)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

bool cmp(pair<int, int> a, pair<int, int> b){
    if(a.second==b.second) return a.first < b.first;
    else return a.second < b.second;
}

void solution(){
    int N;
    cin >> N;

    vector<pair<int, int> > sessions;
    for(int i=0; i<N; i++){
        int start, end;
        cin >> start >> end;

        sessions.push_back({start, end});
    }

    // 끝나는 시간 기준 정렬
    stable_sort(sessions.begin(), sessions.end(), cmp);

    int end=0;
    int count=0;
    for(auto session: sessions){
        if(session.first >= end){
            // 회의 가능
            count++;
            end = session.second;
        }
    }

    cout<<count<<"\n";
}

bool exists(const char* fileName){
    FILE* fp;
    if((fp = fopen(fileName, "r"))){
        fclose(fp);
        return true;
    }
    return false;
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(NULL);
    cout.tie(NULL);

    if(exists("stdin")){
        freopen("stdin", "r", stdin);
        solution();
        fclose(stdin);
    }
    else{
        solution();
    }

    return 0;
}
```

## JavsScript

```js
const fs = require("fs");
const input = fs.readFileSync("dev/stdin").toString().trim().split("\n");

// 문제 풀이
const N = +input[0];
const sessions = input
  .filter((v, i) => i > 0)
  .map((v) => v.split(" ").map((v) => +v));

// 끝나는 시간 기준으로 오름차순 정렬
sessions.sort((a, b) => {
  if (a[1] === b[1]) return a[0] - b[0];
  else return a[1] - b[1];
});

let count = 1;
let end = sessions[0][1];
for (let i = 1; i < sessions.length; i++) {
  const session = sessions[i];

  // 아직 회의 진행중이라 회의 진행 불가
  if (end > session[0]) continue;

  // 회의 진행
  end = session[1];
  count++;
}

console.log(count);
```

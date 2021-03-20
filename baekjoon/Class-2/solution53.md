---
title: "덩치(7568)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-20"
---

## 문제 링크

[덩치(7568)](https://www.acmicpc.net/problem/7568)

## C++

```cpp
#include <iostream>
#include <vector>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, a, b;
    cin >> n;
    vector<vector<int> > xyVec(n, vector<int>(2));
    int idx=0;
    while(cin >> a >> b){
        xyVec[idx][0]=a;
        xyVec[idx][1]=b;
        idx++;
    }

    string rank="";
    for(int i=0; i<n; i++){
        int x = xyVec[i][0];
        int y = xyVec[i][1];

        int cnt=0;
        for(int j=0; j<n; j++){
            if(i==j) continue;
            int otherX = xyVec[j][0];
            int otherY = xyVec[j][1];
            if(otherX > x && otherY > y)
                cnt++;
        }
        rank += to_string(cnt+1) + " ";
    }
    rank.pop_back();    // 마지막 공백 제거

    cout<<rank<<endl;
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
// split 조절
const input = fs.readFileSync("dev/stdin").toString().trim().split("\n");

// 문제 풀이
const n = +input[0];
const xyList = input
  .filter((v, i) => i > 0)
  .map((v) => v.split(" ").map((v) => +v));

const rank = [];
xyList.forEach((xy, idx) => {
  let cnt = 1;
  const x = xy[0];
  const y = xy[1];
  xyList.forEach((others, i) => {
    if (idx !== i) {
      // 다른 사람과 비교
      const otherX = others[0];
      const otherY = others[1];
      if (otherX > x && otherY > y) cnt++;
    }
  });
  rank.push(cnt);
});

console.log(rank.join(" "));
```

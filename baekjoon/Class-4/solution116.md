---
title: "스티커(9465)"
category: 백준[Class-4]
tags: [C++, JavaScript, 백준]
date: "2021-05-29"
---

## 문제 링크

[스티커(9465)](https://www.acmicpc.net/problem/9465)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

// 문제 풀이
void solution(){
    int t;
    cin >> t;

    for(int i=0; i<t; i++){
        int n;
        cin >> n;

        // Init
        vector<vector<int> > stickers;
        for(int j=0; j<2; j++){
            vector<int> vec;

            vec.push_back(0);   // 0번 째 추가
            for(int k=0; k<n; k++){
                int x;
                cin >> x;

                vec.push_back(x);
            }

            stickers.push_back(vec);
        }

        // DP
        if(n==1){
            cout<<max(stickers[0][1], stickers[1][1])<<"\n";
        }
        else {
            for(int k=2; k<=n; k++){
                // 0행 k열 뽑을 경우, 1행 k-1열과 1행 k-2열 중 큰 값과 0행 k열 뽑을 경우를 더함.
                stickers[0][k] = max(stickers[1][k-1], stickers[1][k-2]) + stickers[0][k];
                // 1행 k열 뽑을 경우, 0행 k-1열과 0행 k-2열 중 큰 값과 1행 k열 뽑을 경우를 더함.
                stickers[1][k] = max(stickers[0][k-1], stickers[0][k-2]) + stickers[1][k];
            }

            cout<<max(stickers[0][n], stickers[1][n])<<"\n";
        }
    }
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

// Function

// 문제 풀이
let cursor = 0;
const t = +input[cursor++];

for (let i = 0; i < t; i++) {
  const n = +input[cursor++];
  const stickers = [];
  stickers.push(input[cursor++].split(" "));
  stickers.push(input[cursor++].split(" "));
  stickers[0].unshift(0);
  stickers[1].unshift(0);

  if (n >= 2) {
    // string -> int
    stickers[0][1] = +stickers[0][1];
    stickers[1][1] = +stickers[1][1];

    for (let k = 2; k <= n; k++) {
      // string -> int
      stickers[0][k] = +stickers[0][k];
      stickers[1][k] = +stickers[1][k];

      // dp
      stickers[0][k] += Math.max(stickers[1][k - 1], stickers[1][k - 2]);
      stickers[1][k] += Math.max(+stickers[0][k - 1], +stickers[0][k - 2]);
    }
  }

  console.log(Math.max(stickers[0][n], stickers[1][n]));
}
```

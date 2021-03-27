---
title: "프린터 큐(1966)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-27"
---

## 문제 링크

[프린터 큐(1966)](https://www.acmicpc.net/problem/1966)

## C++

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <algorithm>

using namespace std;

// 문제 풀이 함수
void solution(){
    int k;
    cin >> k;
    for(int i=0; i<k; i++){
        int n, m;
        cin >> n >> m;

        queue<pair<int, int> > q;
        vector<int> priority(n);
        for(int j=0; j<n; j++){
            int a;
            cin >> a;
            priority[j]=a;
            q.push({j, a}); // {index, priority}
        }

        // 내림차순 정렬
        stable_sort(priority.rbegin(), priority.rend());

        int cnt=0;
        while(!q.empty()){
            int idx = q.front().first;
            int prio = q.front().second;
            q.pop();

            if(priority[cnt] > prio)
                q.push({idx, prio});
            else{
                cnt++;  // 다음 우선 순위
                if(idx==m) break;   // 찾던 인덱스
            }
        }
        cout<<cnt<<"\n";
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
const k = +input[0];
const log = [];
for (let i = 1; i < k + k; i += 2) {
  input[i] = input[i].split(" ");

  const n = +input[i][0];
  const m = +input[i][1];

  const priority = input[i + 1].split(" ").map((v) => +v);
  const queue = priority.map((v, i) => [i, v]);

  // 내림차순 정렬
  priority.sort((a, b) => b - a);

  let cnt = 0;
  while (queue.length > 0) {
    const idx = queue[0][0];
    const prio = queue[0][1];
    queue.shift();

    if (prio < priority[cnt]) {
      queue.push([idx, prio]);
    } else {
      cnt++; // 다음 우선순위
      if (idx === m) break; // 찾으려던 인덱스
    }
  }
  log.push(cnt);
}

console.log(log.join("\n"));
```

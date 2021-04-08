---
title: "바이러스(2606)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-04-08"
---

## 문제 링크

[바이러스(2606)](https://www.acmicpc.net/problem/2606)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <map>

using namespace std;

int findRoot(map<int, int>& roots, int num){
    if(roots[num] == num) return num;
    else return roots[num]=findRoot(roots, roots[num]);
}

// 문제 풀이 함수
void solution(){
    int numLen, linkLen;
    cin >> numLen >> linkLen;

    map<int, int> roots;
    for(int i=1; i<=numLen; i++){
        roots[i] = i;
    }

    for(int i=0; i<linkLen; i++){
        int cpt1, cpt2;
        cin >> cpt1 >> cpt2;

        int rootCpt1 = findRoot(roots, cpt1);
        int rootCpt2 = findRoot(roots, cpt2);

        // 작은 쪽으로 root 지정
        roots[max(rootCpt1, rootCpt2)] = min(rootCpt1, rootCpt2);
    }

    int cnt=0;
    for(int i=2; i<=numLen; i++){
        if(findRoot(roots, i)==1)
            cnt++;
    }
    cout<<cnt;
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
const cptCnt = +input[0];
const linkCnt = +input[1];
const links = input
  .filter((v, i) => i > 1)
  .map((v) => v.split(" ").map((v) => +v));

const findRoot = (root, num) => {
  if (root[num] === num) return num;
  else return (root[num] = findRoot(root, root[num]));
};

const root = {};
for (let i = 1; i <= cptCnt; i++) {
  // 처음에 자신을 root로
  root[i] = i;
}

links.forEach((v) => {
  const cpt1 = v[0];
  const cpt2 = v[1];
  const rootCpt1 = findRoot(root, cpt1);
  const rootCpt2 = findRoot(root, cpt2);

  // 작은 쪽을 root로
  root[Math.max(rootCpt1, rootCpt2)] = Math.min(rootCpt1, rootCpt2);
});

let cnt = 0; // 1번 컴퓨터 제외
for (let i = 2; i <= cptCnt; i++) {
  if (findRoot(root, i) === 1) cnt++;
}
console.log(cnt);
```

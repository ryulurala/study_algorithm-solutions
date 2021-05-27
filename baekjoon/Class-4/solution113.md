---
title: "N과 M (2)(15650)"
category: 백준[Class-4]
tags: [C++, JavaScript, 백준]
date: "2021-05-27"
---

## 문제 링크

[N과 M (2)(15650)](https://www.acmicpc.net/problem/15650)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

void doCombination(vector<int>& origin, vector<bool>& selected, int select, int start){
    if(select == 0){
        for(int i=0; i<selected.size(); i++){
            if(!selected[i]) continue;

            // 출력만
            cout<<origin[i]<<" ";
        }
        cout<<"\n";
    }
    else {
        for(int i=start; i<origin.size(); i++){
            if(selected[i]) continue;

            selected[i] = true;
            doCombination(origin, selected, select-1, i);
            selected[i] = false;
        }
    }
}

// 문제 풀이
void solution(){
    int n, m;
    cin >> n >> m;

    vector<int> nums(n, 0);
    for(int i=1; i<=n; i++){
        nums[i-1] = i;
    }

    // Combination
    vector<bool> selected(n, false);
    doCombination(nums, selected, m, 0);
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
const doCombi = (origin, select) => {
  const result = [];

  if (select === 1) {
    return origin.map((v) => [v]);
  } else {
    origin.forEach((v, i) => {
      const fixed = v;
      const sliceArr = origin.slice(i + 1);
      const combiArr = doCombi(sliceArr, select - 1);
      const mergeArr = combiArr.map((vv) => [fixed, ...vv]);
      result.push(...mergeArr);
    });

    return result;
  }
};

// 문제 풀이
const [n, m] = input[0].split(" ");

const origin = Array.from({ length: +n }, (v, i) => i + 1);

const result = doCombi(origin, +m);

console.log(result.map((v) => v.join(" ")).join("\n"));
```

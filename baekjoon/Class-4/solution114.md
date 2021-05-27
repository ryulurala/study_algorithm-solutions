---
title: "N과 M (5)"
category: 백준[Class-4]
tags: [C++, JavaScript, 백준]
date: "2021-05-27"
---

## 문제 링크

[N과 M (5)(15654)](https://www.acmicpc.net/problem/15654)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

void doPermutation(vector<int>& origin, vector<bool>& selected, int select, vector<int>& stack){
    if(select == 0){
        for(int e: stack){
            cout<<e<<" ";
        }
        cout<<"\n";
    }
    else {
        for(int i=0; i<origin.size(); i++){
            if(selected[i]) continue;

            selected[i] = true;
            stack.push_back(origin[i]); // 후입선출
            doPermutation(origin, selected, select-1, stack);
            stack.pop_back();
            selected[i] = false;
        }
    }
}

// 문제 풀이
void solution(){
    int n, m;
    cin >> n >> m;

    vector<int> nums(n, 0);
    for(int i=0; i<n; i++){
        cin >> nums[i];
    }

    // 오름차순 정렬
    stable_sort(nums.begin(), nums.end());

    // Permutation
    vector<bool> selected(n, false);
    vector<int> stack;
    doPermutation(nums, selected, m, stack);
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
const doPermu = (origin, select) => {
  const result = [];

  if (select === 1) {
    return origin.map((v) => [v]);
  } else {
    origin.forEach((v, i) => {
      const fixed = v;
      const filterArr = origin.filter((vv, ii) => ii !== i);
      const permuArr = doPermu(filterArr, select - 1);
      const mergeArr = permuArr.map((vv) => [fixed, ...vv]);
      result.push(...mergeArr);
    });

    return result;
  }
};

// 문제 풀이
const [n, m] = input[0].split(" ");

const origin = input[1].split(" ").map((v) => +v);
origin.sort((a, b) => a - b);

const result = doPermu(origin, +m);

console.log(result.map((v) => v.join(" ")).join("\n"));
```

---
title: "좌표 압축(18870)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-05-22"
---

## 문제 링크

[좌표 압축(18870)](https://www.acmicpc.net/problem/18870)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
#include <set>

using namespace std;

int doBst(vector<int>& vec, int target){
    int left = 0;
    int right = vec.size()-1;

    while(left < right){
        int mid = (left + right) / 2;

        if(vec[mid] == target){
            left = mid;
            break;
        }
        else if(vec[mid] < target){
            left = mid+1;
        }
        else if(vec[mid] > target){
            right = mid-1;
        }
    }

    return left;
}

void solution(){
    int n;
    cin >> n;

    vector<int> origin;
    set<int> s;
    for(int i=0; i<n; i++){
        int x;
        cin >> x;

        origin.push_back(x);
        s.insert(x);    // 중복 제거, 정렬
    }

    vector<int> vec(s.begin(), s.end());
    for(int e: origin){
        // BST
        int index = doBst(vec, e);
        cout<<index<<" ";
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

const doBst = (array, target) => {
  let left = 0;
  let right = array.length - 1;

  while (left < right) {
    const mid = Math.floor((left + right) / 2);

    if (array[mid] < target) {
      left = mid + 1;
    } else if (array[mid] > target) {
      right = mid - 1;
    } else {
      left = mid;
      break;
    }
  }

  return left;
};

// 문제 풀이
const n = +input[0];
input[1] = input[1].split(" ").map((v) => +v);

// 오름차순 정렬 및 중복 제거
let array = [...input[1]];
array.sort((a, b) => a - b);
array = array.filter((v, i, arr) => i === 0 || v !== arr[i - 1]);

const log = [];
for (const e of input[1]) {
  // BST
  const index = doBst(array, e);
  log.push(index);
}

console.log(log.join(" "));
```

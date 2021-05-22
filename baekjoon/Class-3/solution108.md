---
title: "Z(1074)"
category: 백준[Class-3]
tags: [C++, JavaScript, 백준]
date: "2021-05-23"
---

## 문제 링크

[Z(1074)](https://www.acmicpc.net/problem/1074)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

int n, r, c;
int mark;

void divide(int size, int row, int col){
    if(r==row && c==col){
        // 원하는 위치
        cout<<mark<<"\n";
    }
    else if(r>=row && r<row+size && c>=col && c<col+size){
        // 해당 면에 포함되므로 4분할
        size /= 2;
        divide(size, row, col);
        divide(size, row, col+size);
        divide(size, row+size, col);
        divide(size, row+size, col+size);
    }
    else {
        // 해당 4분면에 포함되지 않음.
        mark += (size*size);
    }
}

void solution(){
    cin >> n >> r >> c;

    int size = 1 << n;
    mark = 0;
    divide(size, 0, 0);
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
input[0] = input[0].split(" ");
const [n, r, c] = [+input[0][0], +input[0][1], +input[0][2]];

let mark = 0;
const divide = (size, row, col) => {
  if (r === row && c === col) {
    // 위치 찾음.
    console.log(mark);
  } else if (r >= row && r < row + size && c >= col && c < col + size) {
    // 사분면에 포함 [0]
    size /= 2;
    divide(size, row, col);
    divide(size, row, col + size);
    divide(size, row + size, col);
    divide(size, row + size, col + size);
  } else {
    // 사분면에 포함 [x]
    mark += size * size;
  }
};

const size = 1 << n;
divide(size, 0, 0);
```

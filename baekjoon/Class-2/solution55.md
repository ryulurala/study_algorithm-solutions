---
title: "수 정렬하기 3(10989)"
category: 백준[Class-2]
tags: [C++, JavaScript, 백준]
date: "2021-03-21"
---

## 문제 링크

[수 정렬하기 3(10989)](https://www.acmicpc.net/problem/10989)

## C++

```cpp
#include <iostream>

using namespace std;

// 문제 풀이 함수
void solution(){
    int n, a;
    scanf("%d", &n);
    int counts[10001]={0, };
    while(scanf("%d", &a)!= EOF){
        counts[a]++;
    }

    for(int i=1; i<10001; i++){
        for(int j=0; j<counts[i]; j++){
            printf("%d\n", i);
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

- 이 코드는 통과하지 못했다.
  - [백준] 에서 `node.js`의 메모리 범위를 `Java`, `Kotlin`처럼 메모리를 늘려주지 않는 이상은 불가능하다고 생각된다.
  - 위에 `C++` 코드와 로직은 같다.(= counting sort)

```js
const fs = require("fs");
// split 조절
const input = fs.readFileSync("dev/stdin").toString().trim().split("\n");

// 문제 풀이
const n = +input[0];
const nums = [];
for (let i = 1; i <= n; i++) {
  nums.push(+input[i]);
}

const countNums = Array.from({ length: 10001 }, () => 0);

nums.forEach((v) => {
  countNums[v]++;
});

let print = "";
for (let i = 1; i < countNums.length; i++) {
  const num = i;
  const count = countNums[i];
  if (count > 0) {
    print += (num + "\n").repeat(count);
  }
}
console.log(print.trim());
```

---
title: "곱셈(1629)"
category: 백준[Class-4]
tags: [C++, JavaScript, 백준]
date: "2021-06-10"
---

## 문제 링크

[곱셈(1629)](https://www.acmicpc.net/problem/1629)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

long long pow(int a, int b, int c){
    if(b > 1){
        long long half = pow(a, b/2, c)%c;

        if(b%2==0)
            return half*half%c;     // b가 짝수
        else
            return half*half%c*a%c;   // b가 홀수
    }
    else return a;
}

// 문제 풀이
void solution(){
    int a, b, c;
    cin >> a >> b >> c;

    cout<<pow(a%c, b, c)<<"\n";
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

// 함수
const pow = (a, b, c) => {
  if (b > 1n) {
    const half = pow(a, BigInt(parseInt(b / 2n)), c) % c;

    if (b % 2n === 0n) return (half * half) % c;
    else return (((half * half) % c) * a) % c;
  } else return a % c;
};

// 문제 풀이
const [a, b, c] = input[0].split(" ");

console.log(parseInt(pow(BigInt(+a), BigInt(+b), BigInt(+c))));
```

---
title: "조합(2407)"
category: 백준[Class-4]
tags: [C++, JavaScript, 백준]
date: "2021-05-27"
---

## 문제 링크

[조합(2407)](https://www.acmicpc.net/problem/2407)

## C++

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

string add_num(string num1, string num2){
    string result = "";
    int sum = 0;

    while(!num1.empty() || !num2.empty() || sum>0){
        if(!num1.empty()){
            sum += num1.back() - '0';
            num1.pop_back();
        }

        if(!num2.empty()){
            sum += num2.back() - '0';
            num2.pop_back();
        }

        result += to_string(sum%10);    // 일의 자리만
        sum /= 10;
    }
    reverse(result.begin(), result.end());  // 뒤집기

    return result;
}

// 문제 풀이
void solution(){
    int n, m;
    cin >> n >> m;

    vector<vector<string> > dp(n+1, vector<string>(n+1, "0"));
    dp[0][0] = "1";
    dp[1][0] = "1";
    dp[1][1] = "1";

    // n C r = n-1 C r + n-1 C r-1
    for(int a=2; a<=n; a++){
        for(int b=0; b<=a; b++){
            if(a==b || b==0) dp[a][b] = "1";
            else dp[a][b] = add_num(dp[a-1][b], dp[a-1][b-1]);
        }
    }

    cout<<dp[n][m]<<"\n";
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
const add_bigNum = (num1, num2) => {
  let result = "";
  let sum = 0;

  while (num1.length > 0 || num2.length > 0 || sum > 0) {
    if (num1.length > 0) {
      sum += +num1[num1.length - 1];
      num1 = num1.slice(0, -1);
    }

    if (num2.length > 0) {
      sum += +num2[num2.length - 1];
      num2 = num2.slice(0, -1);
    }

    result += (sum % 10).toString(); // 일의 자리
    sum = Math.floor(sum / 10);
  }
  result = result.split("").reverse().join(""); // 뒤집기

  return result;
};

// 문제 풀이
const [n, m] = input[0].split(" ");

const dp = Array.from({ length: n + 1 }, () =>
  Array.from({ length: n + 1 }, () => "0")
);

dp[0][0] = dp[1][0] = dp[1][1] = "1";

for (let i = 2; i <= n; i++) {
  for (let j = 0; j <= i; j++) {
    if (i === j || j === 0) {
      dp[i][j] = "1";
    } else {
      // n C r = n-1 C r + n-1 C r-1
      dp[i][j] = add_bigNum(dp[i - 1][j], dp[i - 1][j - 1]);
    }
  }
}

console.log(dp[n][m]);
```

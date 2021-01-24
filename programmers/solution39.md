---
title: "직사각형 별찍기"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[직사각형 별찍기](https://programmers.co.kr/learn/courses/30/lessons/12969)

### C++

```cpp
#include <iostream>

using namespace std;

int main(void) {
    int n;
    int m;
    cin >> n >> m;

    for(int i=0; i<m; i++){
        for(int j=0; j<n; j++){
            printf("*");
        }
        cout<<endl;
    }

    return 0;
}
```

### JavaScript

```js
process.stdin.setEncoding("utf8");
process.stdin.on("data", (data) => {
  const n = data.split(" ");
  const a = Number(n[0]),
    b = Number(n[1]);

  let str = "";
  for (let i = 0; i < b; i++) {
    for (let j = 0; j < a; j++) {
      str += "*";
    }
    str += "\n";
  }

  console.log(str);
});
```

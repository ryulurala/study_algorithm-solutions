---
title: "서울에서 김서방 찾기"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-20"
---

## 문제 링크

[서울에서 김서방 찾기](https://programmers.co.kr/learn/courses/30/lessons/12919)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

string solution(vector<string> seoul) {
    string answer = "";

    answer += "김서방은 ";
    for(int i=0; i<seoul.size(); i++){
        if(seoul[i] != "Kim") continue;
        answer += to_string(i);
        break;
    }
    answer += "에 있다";

    return answer;
}
```

### JavaScript

```js
function solution(seoul) {
  var answer = "";

  answer += "김서방은 " + seoul.indexOf("Kim") + "에 있다";

  return answer;
}
```

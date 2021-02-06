---
title: "신규 아이디 추천"
category: 프로그래머스[Level-1]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-06"
---

## 문제 링크

[신규 아이디 추천](https://programmers.co.kr/learn/courses/30/lessons/72410)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

string solution(string new_id) {
    string answer = "";

    // 1단계
    string id1="";
    for(char ch: new_id) id1+=tolower(ch);

    // 2단계
    string id2="";
    for(char ch: id1){
        if(ch>='0'&&ch<='9') id2+=ch;
        else if(ch>='a'&&ch<='z') id2+=ch;
        else if(ch=='-'||ch=='_'|ch=='.') id2+=ch;
    }

    // 3단계
    string id3="";
    for(char ch: id2){
        if(ch=='.'&&id3.back()=='.') continue;
        id3+=ch;
    }

    // 4단계
    string id4(id3);
    while(id4.front()=='.') id4=id4.substr(1);
    while(id4.back()=='.') id4.pop_back();

    // 5단계
    string id5=(id4=="")?"a":id4;

    // 6단계
    string id6=id5.substr(0, 15);
    while(id6.back()=='.') id6.pop_back();

    // 7단계
    string id7(id6);
    while(id7.length()<3) id7+=id7.back();

    // 대입
    answer=id7;

    return answer;
}
```

### JavaScript

```js
function solution(new_id) {
  var answer = "";

  answer = new_id
    .toLowerCase() // 1단계
    .replace(/[^a-z-_.0-9]/g, "") // 2단계
    .replace(/[.]+/g, ".") // 3단계
    .replace(/^[.]|[.]$/, "") // 4단계
    .replace(/^$/, "a") // 5단계
    .slice(0, 15) // 6.1단계
    .replace(/[.]$/, ""); // 6.2단계

  while (answer.length < 3) {
    answer += answer[answer.length - 1]; // 7단계
  }

  return answer;
}
```

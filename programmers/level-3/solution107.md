---
title: "여행경로"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-06"
---

## 문제 링크

[여행경로](https://programmers.co.kr/learn/courses/30/lessons/43164)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

string result="";

void dfsGo(vector<vector<string>>& tickets, string total, vector<bool>& visited){
    if(total.length()/3==tickets.size()+1){
        if(result.empty()||total<result){   // 알파벳 순서
            result=total;
        }
    }
    else{
        for(int i=0; i<tickets.size(); i++){
            if(!visited[i]&&tickets[i][0]==total.substr(total.length()-3)){
                visited[i]=true;
                dfsGo(tickets, total+tickets[i][1], visited);
                visited[i]=false;
            }
        }
    }
}

vector<string> solution(vector<vector<string>> tickets) {
    vector<string> answer;

    vector<bool> visited(tickets.size(), false);
    for(int i=0; i<tickets.size(); i++){
        if(tickets[i][0]=="ICN"){
            visited[i]=true;
            dfsGo(tickets, "ICN"+tickets[i][1], visited);
            visited[i]=false;
        }
    }

    for(int i=0; i<result.length(); i+=3){
        answer.push_back(result.substr(i, 3));
    }

    return answer;
}
```

### JavaScript

```js
function solution(tickets) {
  var answer = [];

  let result = "";
  const dfsGo = (total, visited) => {
    if (total.length / 3 === tickets.length + 1) {
      if (result.length === 0 || total < result) {
        // 비어있거나 알파벳순
        result = total;
      }
    } else {
      for (let i = 0; i < tickets.length; i++) {
        if (!visited[i] && tickets[i][0] === total.slice(-3)) {
          visited[i] = true;
          dfsGo(total + tickets[i][1], visited);
          visited[i] = false;
        }
      }
    }
  };

  const visited = Array.from({ length: tickets.length }, () => false);
  for (let i = 0; i < tickets.length; i++) {
    if (tickets[i][0] === "ICN") {
      visited[i] = true;
      dfsGo("ICN" + tickets[i][1], visited);
      visited[i] = false;
    }
  }
  answer = result.match(/\w{3}/g); // 3칸씩 나누기

  return answer;
}
```

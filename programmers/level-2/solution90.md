---
title: "오픈채팅방"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-02"
---

## 문제 링크

[오픈채팅방](https://programmers.co.kr/learn/courses/30/lessons/42888)

### C++

```cpp
#include <string>
#include <vector>
#include <map>
#include <sstream>

using namespace std;

vector<string> solution(vector<string> record) {
    vector<string> answer;

    map<string, string> uid_nick;
    vector<string> order;
    for(string str: record){
        // split
        stringstream ss(str);
        string doing, uid, nick;
        ss>>doing;
        ss>>uid;
        switch(doing[0]){
            case 'E':{
                ss>>nick;
                uid_nick[uid]=nick;
                order.push_back(uid);
                order.push_back("님이 들어왔습니다.");
            }
                break;
            case 'L':{
                order.push_back(uid);
                order.push_back("님이 나갔습니다.");
            }
                break;
            case 'C':{
                ss>>nick;
                uid_nick[uid]=nick;
            }
                break;
        }
    }

    // 메시지 배열
    for(int i=0; i<order.size(); i+=2){
        string nick=uid_nick[order[i]];
        string doing=order[i+1];

        answer.push_back(nick+doing);
    }

    return answer;
}
```

### JavaScript

```js
function solution(record) {
  var answer = [];

  const uid_nick = new Map();
  record.forEach((val) => {
    val = val.split(" ");
    switch (val[0][0]) {
      case "E":
        {
          uid_nick.set(val[1], val[2]);
          answer.push(val[1] + "님이 들어왔습니다.");
        }
        break;
      case "L":
        {
          answer.push(val[1] + "님이 나갔습니다.");
        }
        break;
      case "C":
        {
          uid_nick.set(val[1], val[2]);
        }
        break;
    }
  });

  answer = answer.map((val) => {
    return val.replace(/\w+/, (v) => uid_nick.get(v));
  });

  return answer;
}
```

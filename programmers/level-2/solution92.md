---
title: "방금그곡"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-03"
---

## 문제 링크

[방금그곡](https://programmers.co.kr/learn/courses/30/lessons/17683)

### C++

```cpp
#include <string>
#include <vector>
#include <sstream>

using namespace std;

string code2lower(string str){
    string s="";
    for(int i=0; i<str.length(); i++){
        if(str[i]=='#') s.back()=tolower(s.back());
        else s+=str[i];
    }
    return s;
}

string solution(string m, vector<string> musicinfos) {
    string answer = "(None)";

    // C# => c
    m=code2lower(m);

    int maxTime=0;
    for(string music: musicinfos){
        // split
        stringstream ss(music);
        string str, start, end, title, code;
        int k=0;
        while(getline(ss, str, ',')){
            if(k==0) start=str;
            else if(k==1) end=str;
            else if(k==2) title=str;
            else code=str;
            k++;
        }

        // C# => c
        code=code2lower(code);

        // 시간 간격(분)
        int time=stoi(end.substr(0, 2))*60+stoi(end.substr(3, 2));
        time-=stoi(start.substr(0, 2))*60+stoi(start.substr(3, 2));

        // 코드 흐름
        string flow="";
        for(int i=0; i<time; i++){
            flow+=code[i%code.length()];
        }

        // 일치하는지, 재생된 시간이 제일 긴지
        if(flow.find(m)!=string::npos && time>maxTime){
            answer=title;
            maxTime=time;
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(m, musicinfos) {
  var answer = "(None)";

  // C# => c
  m = m.replace(/[A-Z]#/g, (v) => v[0].toLowerCase());

  let maxTime = 0;
  musicinfos.forEach((music) => {
    // split
    music = music.split(",");
    const start = music[0].split(":");
    const end = music[1].split(":");
    const title = music[2];
    const code = music[3].replace(/[A-Z]#/g, (v) => v[0].toLowerCase());

    // 시간 계산
    const time = (+end[0] - start[0]) * 60 + (+end[1] - start[1]);

    // 전체 멜로디
    let flow = "";
    for (let i = 0; i < time; i++) {
      flow += code[i % code.length];
    }

    // 일치하는지, 제일 긴 길이인지
    if (flow.includes(m) && time > maxTime) {
      answer = title;
      maxTime = time;
    }
  });

  return answer;
}
```

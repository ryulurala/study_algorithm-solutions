---
title: "셔틀버스"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-27"
---

## 문제 링크

[셔틀버스](https://programmers.co.kr/learn/courses/30/lessons/17678)

### C++

```cpp
#include <string>
#include <vector>
#include <queue>
#include <iostream>

using namespace std;

int toInt(string time){
    int hour = stoi(time.substr(0, 2));
    int min = stoi(time.substr(3, 2));

    return hour*60 + min;
}

string toStr(int time){
    string ret="";
    int hour = time/60;
    ret += hour<10 ? '0'+to_string(hour):to_string(hour);
    ret += ':';
    int min = time%60;
    ret += min<10 ? '0'+to_string(min):to_string(min);

    return ret;
}

string solution(int n, int t, int m, vector<string> timetable) {
    string answer = "";

    // init
    priority_queue<int, vector<int>, greater<int> > pq;
    for(string time: timetable)
        pq.push(toInt(time));

    int start = toInt("09:00");
    for(int i=0; i<n; i++){
        answer=toStr(start);    // 일단 제일 늦게 오기
        int last;
        int cnt=0;
        while(!pq.empty()){
            // 탑승
            last = pq.top();
            if(last>start) break;
            pq.pop();
            cnt++;
            if(cnt==m) break;
        }
        // 만차일 경우, 마지막 사람보다 1분 빠르게
        if(cnt==m) answer=toStr(last-1);
        start+=t;   // next
    }

    return answer;
}
```

### JavaScript

```js
function solution(n, t, m, timetable) {
  var answer = "";

  const toStr = (time) => {
    let ret = "";
    const hour = parseInt(time / 60);
    ret += hour < 10 ? "0" + hour : hour;
    ret += ":";
    const min = time % 60;
    ret += min < 10 ? "0" + min : min;

    return ret;
  };

  const toInt = (time) => {
    const hour = +time.slice(0, 2);
    const min = +time.slice(3);

    return hour * 60 + min;
  };

  // 오름차순 + toInt
  timetable = timetable
    .sort((a, b) => toInt(a) - toInt(b))
    .map((v) => toInt(v));

  let start = toInt("09:00");
  let idx = 0;
  for (let i = 0; i < n; i++) {
    answer = toStr(start); // 일단 제일 늦게 오기
    let cnt = 0;
    while (idx < timetable.length) {
      // 탑승
      const last = timetable[idx];
      if (last > start || cnt === m) break;
      idx++;
      cnt++;
    }
    // 만차일 경우, 마지막 사람보다 1분 빠르게
    if (cnt === m) answer = toStr(timetable[idx - 1] - 1);
    start += t;
  }

  return answer;
}
```

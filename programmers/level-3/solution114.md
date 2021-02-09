---
title: "광고 삽입"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-09"
---

## 문제 링크

[광고 삽입](https://programmers.co.kr/learn/courses/30/lessons/72414)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

int toSec(string str){
    int second=stoi(str.substr(0, 2))*3600
    +stoi(str.substr(3, 2))*60
    +stoi(str.substr(6, 2));

    return second;
}

string toStr(int second){
    string str="";

    // 시
    int hour=second/3600;
    second%=3600;
    if(hour<10) str+='0';
    str+=to_string(hour)+':';

    // 분
    int minute=second/60;
    second%=60;
    if(minute<10) str+='0';
    str+=to_string(minute)+':';

    // 초
    if(second<10) str+='0';
    str+=to_string(second);

    return str;
}

string solution(string play_time, string adv_time, vector<string> logs) {
    string answer = "";

    if(play_time==adv_time) return "00:00:00";

    // init(변환)
    int playTime=toSec(play_time);
    int advTime=toSec(adv_time);

    vector<int> viewer(playTime+1, 0);  // 시청자 수
    for(string log: logs){
        int start=toSec(log.substr(0, 8));
        int end=toSec(log.substr(9, 8));

        for(int i=start; i<end; i++) viewer[i]++;
    }

    long long curTime=0;    // 시작 시간이 00:00:00 일 때, 누적 재생 시간
    for(int i=0; i<advTime; i++) curTime+=viewer[i];

    long long maxTime=0;
    int startTime=0;
    maxTime=curTime;
    for(int i=advTime; i<playTime; i++){
        curTime+=viewer[i];     // 종료 시간 1초씩 증가하면서
        curTime-=viewer[i-advTime]; // 시작 시간 1초씩 증가하면서
        if(curTime>maxTime){
            maxTime=curTime;
            startTime=(i-advTime+1);  // 시작 시간
        }
    }
    answer=toStr(startTime);    // 변환

    return answer;
}
```

### JavaScript

```js

```

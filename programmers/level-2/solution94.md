---
title: "파일명 정렬"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-03"
---

## 문제 링크

[파일명 정렬](https://programmers.co.kr/learn/courses/30/lessons/17686)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <cctype>

using namespace std;

bool cmp(vector<string> a, vector<string> b){
    transform(a[0].begin(), a[0].end(), a[0].begin(), ::tolower);
    transform(b[0].begin(), b[0].end(), b[0].begin(), ::tolower);
    if(a[0]==b[0]) return stoi(a[1])<stoi(b[1]);
    else return a[0]<b[0];
}

vector<string> solution(vector<string> files) {
    vector<string> answer;

    vector<vector<string>> words;
    for(string file: files){
        // split
        vector<string> v;
        int pos=0;

        // HEAD
        for(int i=pos; i<file.length(); i++){
            if(file[i]>='0'&&file[i]<='9'){
                v.push_back(file.substr(0, i));
                pos=i;
                break;
            }
        }

        // NUMBER
        string num="";
        while(pos<file.length()){
            if(file[pos]>='0'&&file[pos]<='9') num+=file[pos++];
            else break;
        }
        v.push_back(num);

        // TAIL
        v.push_back(file.substr(pos));

        words.push_back(v);
    }

    // sort
    stable_sort(words.begin(), words.end(), cmp);

    // push
    for(auto vec: words){
        answer.push_back(vec[0]+vec[1]+vec[2]);
    }

    return answer;
}
```

### JavaScript

```js
function solution(files) {
  var answer = [];

  answer = files
    .map((file) => {
      const matched = file.match(/([^0-9]*)([0-9]*)(.*)/);
      return {
        name: file,
        head: matched[1].toLowerCase(),
        number: +matched[2],
        tail: matched[3],
      };
    })
    .sort((a, b) => {
      if (a.head === b.head && a.number === b.number) return 1;
      // 안바꾸기
      else if (a.head === b.head) return a.number - b.number;
      // 오름차순
      else return a.head < b.head ? -1 : 1; // 사전순
    })
    .map((file) => file.name);

  return answer;
}
```

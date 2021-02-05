---
title: "단어 변환"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-05"
---

## 문제 링크

[단어 변환](https://programmers.co.kr/learn/courses/30/lessons/43163)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>

using namespace std;

bool compare(string a, string b){    // 비교
    int count=0;
    for(int i=0; i<a.length(); i++){
        if(a[i]!=b[i]) count++;
    }
    if(count==1) return true;
    else return false;
}

int bfsGo(string b, string t, vector<string>& w, vector<bool> v, int d){
    if(b==t) return d;
    else{
        int cnt=51;
        for(int i=0; i<w.size(); i++){
            if(!v[i]&&compare(b, w[i])){
                v[i]=true;
                cnt=min(cnt, bfsGo(w[i], t, w, v, d+1));
            }
        }
        return cnt;
    }
}

int solution(string begin, string target, vector<string> words) {
    int answer = 0;

    vector<bool> visited(words.size(), false);

    // bfs
    answer=bfsGo(begin, target, words, visited, 0)%51;

    return answer;
}
```

### JavaScript

```js
function solution(begin, target, words) {
  var answer = 0;

  const compare = (a, b) => {
    let count = 0;
    for (let i = 0; i < a.length; i++) {
      if (a[i] !== b[i]) count++;
    }
    return count === 1 ? true : false;
  };

  const bfsGo = (current, visited, depth) => {
    if (current === target) return depth;
    else {
      let count = 51;
      for (let i = 0; i < words.length; i++) {
        if (!visited[i] && compare(current, words[i])) {
          visited[i] = true;
          count = Math.min(count, bfsGo(words[i], visited.slice(), depth + 1));
        }
      }
      return count;
    }
  };

  const visited = Array.from({ length: words.length }, () => false);

  // bfs
  answer = bfsGo(begin, visited, 0) % 51;

  return answer;
}
```

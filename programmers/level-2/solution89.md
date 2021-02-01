---
title: "캐시"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-01"
---

## 문제 링크

[캐시](https://programmers.co.kr/learn/courses/30/lessons/17680)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

int solution(int cacheSize, vector<string> cities) {
    int answer = 0;

    vector<string> cache;
    for(string city: cities){
        for(char& ch: city) ch=tolower(ch); // 소문자 변환

        bool isHit=false;
        for(int i=0; i<cache.size(); i++){
            if(cache[i]==city){
                isHit=true;
                cache.push_back(cache[i]);
                cache.erase(cache.begin()+i);
                break;
            }
        }
        if(isHit) answer++;
        else{
            answer+=5;
            cache.push_back(city);
            if(cache.size()>cacheSize) cache.erase(cache.begin());
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(cacheSize, cities) {
  var answer = 0;

  const cache = [];
  cities.forEach((val) => {
    const city = val.slice().toLowerCase(); // 소문자 변환
    const idx = cache.indexOf(city);
    if (idx >= 0) {
      // hit
      answer++;
      cache.splice(idx, 1);
      cache.push(city);
    } else {
      // miss
      answer += 5;
      cache.push(city);
      if (cache.length > cacheSize) cache.shift();
    }
  });

  return answer;
}
```

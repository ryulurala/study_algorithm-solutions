---
title: "영어 끝말잇기"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-01"
---

## 문제 링크

[영어 끝말잇기](https://programmers.co.kr/learn/courses/30/lessons/12981)

### C++

```cpp
#include <string>
#include <vector>
#include <iostream>
#include <set>

using namespace std;

vector<int> solution(int n, vector<string> words) {
    vector<int> answer(2, 0);

    set<string> dict;   // 중복 제거
    int index=1;
    int times=1;
    char back=words.front().front();

    for(string word: words){
        if(dict.count(word)==1||word.front()!=back){
            // 이전에 말하거나 끝말잇기가 아닐 경우
            answer[0]=index;
            answer[1]=times;
            break;
        }
        else{
            dict.insert(word);
            back=word.back();
            if(++index>n){
                times++;
                index%=n;
            }
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(n, words) {
  var answer = [0, 0];

  const dict = new Set(); // 중복 제거
  let index, times;
  index = times = 1;
  let back = words[0][0];

  words.some((word) => {
    if (dict.has(word) || word[0] !== back) {
      // 이전에 말한 단어거나 끝말잇기가 아닐경우
      answer[0] = index;
      answer[1] = times;
      return true; // break;
    } else {
      dict.add(word);
      back = word[word.length - 1];
      if (++index > n) {
        index %= n;
        times++;
      }
    }
  });

  return answer;
}
```

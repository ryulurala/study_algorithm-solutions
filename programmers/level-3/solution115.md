---
title: "가장 긴 팰린드롬"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-10"
---

## 문제 링크

[가장 긴 팰린드롬](https://programmers.co.kr/learn/courses/30/lessons/12904)

### C++

```cpp
#include <iostream>
#include <string>

using namespace std;

bool isPalindrome(string& str, int left, int right){
    while(left<right){
        if(str[left++]!=str[right--]) return false;
    }
    return true;
}

int solution(string s) {
    int answer=0;

    int subLen=s.length();
    while(subLen>0){
        int start=0;    // 부분 문자열 시작 인덱스
        int end=subLen-1;     // 부분 문자열 끝 인덱스
        while(end<s.length()){
            // 부분 문자열 길이만큼 옮김.
            if(isPalindrome(s, start++, end++)) return subLen;
        }
        subLen--;
    }

    return answer;
}
```

### JavaScript

```js
function solution(s) {
  var answer = 0;

  const isPalindrome = (left, right) => {
    while (left < right) {
      if (s[left++] !== s[right--]) return false;
    }
    return true;
  };

  let subLen = s.length; // 부분 문자열 길이
  while (subLen > 0) {
    let start = 0; // 부분 문자열 시작 인덱스
    let end = subLen - 1; // 부분 문자열 끝 인덱스
    while (end < s.length) {
      // 부문 문자열 길이가 일정하게 옮김.
      if (isPalindrome(start++, end++)) return subLen;
    }
    subLen--;
  }

  return answer;
}
```

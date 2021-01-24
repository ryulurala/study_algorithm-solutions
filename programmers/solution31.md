---
title: "키패드 누르기"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-1]
toc: true
toc_sticky: true
---

## 문제 링크

[키패드 누르기](https://programmers.co.kr/learn/courses/30/lessons/67256)

### C++

```cpp
#include <string>
#include <vector>
#include <map>
#include <cmath>
#include <iostream>

using namespace std;

// 시작은 왼손 '*', 오른손 '#'
// 1, 4, 7은 왼손만
// 3, 6, 9는 오른손만
// 2, 5, 8, 0은 가까운 손으로, 거리가 같으면 주손으로

string solution(vector<int> numbers, string hand) {
    string answer = "";

    // 검색할 키패드 생성
    map<char, pair<int, int>> keyPad;
    keyPad['1'] = make_pair(0, 0);
    keyPad['2'] = make_pair(0, 1);
    keyPad['3'] = make_pair(0, 2);
    keyPad['4'] = make_pair(1, 0);
    keyPad['5'] = make_pair(1, 1);
    keyPad['6'] = make_pair(1, 2);
    keyPad['7'] = make_pair(2, 0);
    keyPad['8'] = make_pair(2, 1);
    keyPad['9'] = make_pair(2, 2);
    keyPad['*'] = make_pair(3, 0);
    keyPad['0'] = make_pair(3, 1);
    keyPad['#'] = make_pair(3, 2);

    char left = '*';    // 처음 왼손
    char right = '#';   // 처음 오른손
    for(int e: numbers){
        char num = e + '0';  // ASCII
        if(num=='1' || num=='4' || num=='7'){
            // Only. 왼손
            answer += 'L';
            left = num;     // 갱신
        }
        else if(num=='3' || num=='6' || num=='9'){
            // Only. 오른손
            answer += 'R';
            right = num;    // 갱신
        }
        else{
            // 판별
            int leftDist = abs(keyPad[num].first - keyPad[left].first) +
                abs(keyPad[num].second - keyPad[left].second);

            int rightDist = abs(keyPad[num].first - keyPad[right].first) +
                abs(keyPad[num].second - keyPad[right].second);

            if(leftDist > rightDist){
                answer += 'R';
                right = num;    // 갱신
            }
            else if(leftDist < rightDist){
                answer += 'L';
                left = num;     // 갱신
            }
            else{
                if(hand=="left") left = num;    // 갱신
                else right = num;   // 갱신
                answer += toupper(hand[0]);
            }
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(numbers, hand) {
  var answer = "";

  // 검색할 키패드 생성
  const keyPad = new Map([
    ["1", [0, 0]],
    ["2", [0, 1]],
    ["3", [0, 2]],
    ["4", [1, 0]],
    ["5", [1, 1]],
    ["6", [1, 2]],
    ["7", [2, 0]],
    ["8", [2, 1]],
    ["9", [2, 2]],
    ["*", [3, 0]],
    ["0", [3, 1]],
    ["#", [3, 2]],
  ]);

  let left = "*";
  let right = "#";
  numbers.forEach((value) => {
    value = value.toString();
    if (value === "1" || value === "4" || value === "7") {
      // only. 왼손
      answer += "L";
      left = value; // 갱신
    } else if (value === "3" || value === "6" || value === "9") {
      // only. 오른손
      answer += "R";
      right = value; // 갱신
    } else {
      // 판별
      const leftDist =
        Math.abs(keyPad.get(value)[0] - keyPad.get(left)[0]) +
        Math.abs(keyPad.get(value)[1] - keyPad.get(left)[1]);
      const rightDist =
        Math.abs(keyPad.get(value)[0] - keyPad.get(right)[0]) +
        Math.abs(keyPad.get(value)[1] - keyPad.get(right)[1]);
      if (leftDist > rightDist) {
        answer += "R";
        right = value; // 갱신
      } else if (leftDist < rightDist) {
        answer += "L";
        left = value; // 갱신
      } else {
        if (hand == "left") left = value;
        // 갱신
        else right = value; // 갱신
        answer += hand[0].toUpperCase();
      }
    }
  });

  return answer;
}
```

---
title: "메뉴 리뉴얼"
category: 프로그래머스[Level-2]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-01-27"
---

## 문제 링크

[메뉴 리뉴얼](https://programmers.co.kr/learn/courses/30/lessons/72411)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <map>

using namespace std;

vector<string> solution(vector<string> orders, vector<int> course) {
    vector<string> answer;

    map<string, int> course_count;  // 코스당 주문 횟수
    map<int, int> length_max;   // 조합 길이당 코스 주문 갯수 최대

    for(int len: course){
        length_max[len]=0;  // init
    }

    for(string& str: orders){
        stable_sort(str.begin(), str.end());    // 사전순 정렬
    }

    for(string order: orders){
        for(int len: course){
            if(len>order.length()) break;
            // 조합
            string str(order.length(), '0');
            for(int j=0; j<len; j++){
                str[j]='1';
            }
            do{
                string s="";
                for(int k=0; k<str.length(); k++){
                    if(str[k]=='1'){
                        s+=order[k];
                        if(s.length()==len) break;
                    }
                }
                course_count[s]++;  // 조합 count 증가
                length_max[len]=max(course_count[s], length_max[len]); // maxCount 갱신
            }while(prev_permutation(str.begin(), str.end()));
        }
    }

    for(auto e: course_count){
        if(e.second>1) {
            if(e.second == length_max[e.first.length()])
                answer.push_back(e.first);
        }
    }

    return answer;
}
```

### JavaScript

```js

```

---
title: "수식 최대화"
excerpt: "프로그래머스 풀이"
category: 프로그래머스
tags: [C++, JavaScript, 프로그래머스, Level-2]
toc: true
toc_sticky: true
---

## 문제 링크

[수식 최대화](https://programmers.co.kr/learn/courses/30/lessons/67257)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

long long solution(string expression) {
    long long answer = 0;

    string operations= "*+-";   // ASCII 42, 43, 45
    vector<long long> nums;   // 정수 저장
    vector<char> ops;   // 연산자 저장

    string num = "";
    for(char ch: expression){
        if(ch >= '0' && ch <='9'){
            num += ch;
        }
        else{
            ops.push_back(ch);
            nums.push_back(stoi(num));
            num = "";
        }
    }
    nums.push_back(stoi(num));

    do{
        long long result;   // 결과

        vector<long long> swap1(nums);
        vector<char> swap2(ops);

        for(char op: operations){
            vector<long long> temp1;
            vector<char> temp2;

            int index=0;
            temp1.push_back(swap1[index++]);    // 순서 보장
            for(char ch: swap2){
                temp1.push_back(swap1[index++]);    // 순서 보장
                temp2.push_back(ch);

                if(ch==op){
                    // 연산해야 할 경우

                    long long curr = temp1.back();
                    temp1.pop_back();
                    long long prev = temp1.back();
                    temp1.pop_back();
                    temp2.pop_back();   // 연산자 제거

                    switch(op){
                        case '*': temp1.push_back(prev*curr);
                            break;
                        case '+': temp1.push_back(prev+curr);
                            break;
                        case '-': temp1.push_back(prev-curr);
                            break;
                    }
                }
            }

            swap(temp1, swap1);     // temp1 -> swap1
            swap(temp2, swap2);     // temp2 -> swap2
        }

        result = swap1.back()>0 ? swap1.back() : -swap1.back();
        answer = answer>result ? answer : result;

    }while(next_permutation(operations.begin(), operations.end()));

    return answer;  // 가장 큰 절댓값 금액
}
```

### JavaScript

```js
function solution(expression) {
  var answer = 0;

  const condition = [
    ["*", "+", "-"],
    ["*", "-", "+"],
    ["+", "*", "-"],
    ["+", "-", "*"],
    ["-", "*", "+"],
    ["-", "+", "*"],
  ];
  const exp = expression.split(/([*+-])/g); // split

  condition.forEach((value) => {
    // 우선순위 순회
    const temp = exp.concat(); // 복사

    value.forEach((op) => {
      while (temp.includes(op)) {
        const curr = temp.indexOf(op);
        const prev = temp[curr - 1];
        const next = temp[curr + 1];
        let result;
        switch (op) {
          case "*":
            result = +prev * +next;
            break;
          case "+":
            result = +prev + +next;
            break;
          case "-":
            result = +prev - +next;
            break;
        }
        temp.splice(curr - 1, 3, result.toString()); // 교체
      }
    });

    answer = Math.max(answer, Math.abs(temp[0])); // 비교
  });

  return answer;
}
```

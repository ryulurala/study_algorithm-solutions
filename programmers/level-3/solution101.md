---
title: "자물쇠와 열쇠"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-05"
---

## 문제 링크

[자물쇠와 열쇠](https://programmers.co.kr/learn/courses/30/lessons/60059)

### C++

```cpp
#include <string>
#include <vector>

using namespace std;

void rotate90(vector<vector<int>>& key){
    vector<vector<int>> v(key);
    for(int i=0; i<key.size(); i++){
        for(int j=0; j<key.size(); j++){
            key[i][j]=v[key.size()-1-j][i];
        }
    }
}

vector<vector<int>> createLock(vector<vector<int>>& lock, vector<vector<int>>& key, int x, int y){
    vector<vector<int>> newLock(lock);
    for(int i=0; i<key.size(); i++){
        for(int j=0; j<key.size(); j++){
            newLock[x+i][y+j]^=key[i][j];
        }
    }
    return newLock;
}

bool isUnlocked(vector<vector<int>>& lock, int start, int end){
    for(int i=start; i<end; i++){
        for(int j=start; j<end; j++){
            if(lock[i][j]==0) return false;
        }
    }
    return true;
}

bool solution(vector<vector<int>> key, vector<vector<int>> lock) {
    bool answer = false;

    int keySize=key.size();
    int lockSize=lock.size();

    // zero-padding
    for(int i=0; i<lockSize; i++){
        lock[i].insert(lock[i].begin(), keySize-1, 0);
        lock[i].insert(lock[i].end(), keySize-1, 0);
    }
    vector<int> zero(lock[0].size(), 0);
    lock.insert(lock.begin(), keySize-1, zero);
    lock.insert(lock.end(), keySize-1, zero);

    for(int i=0; i<keySize+lockSize-1; i++){
        for(int j=0; j<keySize+lockSize-1; j++){
            for(int four=0; four<4; four++){
                // XOR로 새로운 lock 생성
                vector<vector<int>> newLock=createLock(lock, key, i, j);
                // 원래의 lock(중앙 부분)에 대해 비교
                if(isUnlocked(newLock, keySize-1, keySize-1+lockSize)) return true;
                // 90도 회전
                rotate90(key);
            }
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(key, lock) {
  var answer = false;

  const rotate90 = (key) => {
    const arr = key.map((v) => [...v]);
    for (let i = 0; i < key.length; i++) {
      for (let j = 0; j < key.length; j++) {
        key[i][j] = arr[key.length - 1 - j][i];
      }
    }
  };

  const createLock = (lock, key, x, y) => {
    const newLock = lock.map((v) => [...v]);
    for (let i = 0; i < key.length; i++) {
      for (let j = 0; j < key.length; j++) {
        newLock[x + i][y + j] ^= key[i][j];
      }
    }

    return newLock;
  };

  const isUnlocked = (lock, start, end) => {
    for (let i = start; i < end; i++) {
      for (let j = start; j < end; j++) {
        if (lock[i][j] === 0) return false;
      }
    }
    return true;
  };

  // zero-padding
  for (let i = 0; i < lock.length; i++) {
    for (let j = 0; j < key.length - 1; j++) {
      lock[i].unshift(0);
      lock[i].push(0);
    }
  }
  for (let j = 0; j < key.length - 1; j++) {
    lock.unshift(lock[0].slice().map(() => 0));
    lock.push(lock[0].slice().map(() => 0));
  }

  // 완전탐색
  for (let i = 0; i < lock.length - key.length + 1; i++) {
    for (let j = 0; j < lock.length - key.length + 1; j++) {
      for (let four = 0; four < 4; four++) {
        // XOR로 새로운 배열 생성
        const newLock = createLock(lock, key, i, j);
        // 비교
        if (isUnlocked(newLock, key.length - 1, lock.length - key.length + 1))
          return true;
        // 90도 회전
        rotate90(key);
      }
    }
  }

  return answer;
}
```

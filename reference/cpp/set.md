---
title: "C++ set Header"
excerpt: "<set> of C++"
category: Cpp-Reference
tags: [C++, set, multiset]
toc: true
---

## set, multiset of C++

- `#include <set>`

  > 집합(`set`) 용으로 사용 vs `map`(key로 value 검색)  
  > Only. key로 이루어짐.  
  > 중복 불가능: `set`  
  > 중복 가능: `multiset`(`<set>` 에 존재)  
  > 삽입 후 key 값으로 자동 오름차순(디폴트) 정렬

- 생성자(`set`)

```cpp
#include <set>    // 헤더 선언

// set(중복 불가능)
set<key> s;      // 기본 set 선언(insert(key)로 삽입)
set<key> s2(s1);  // s2를 선언(s1을 복사한), =복사생성자
set<key, less<key>> s;   // key 값 내림차순 자동 정렬 set 선언
```

- 생성자(`multiset`)

```cpp
#include <set>

// multiset(중복 가능)
multiset<key> ms;    // 기본 multiset 선언(insert(key)로 삽입)
multiset<key, less<key>> ms;  // key 값으로 내림차순 자동 정렬되는 중복 가능 set 선언
```

- 멤버 함수(`set`)

```cpp
#include <set>

set<key> s;

s.find(key); // 해당 key 값과 일치하는 iterator(반복자) 반환, 없다면 s.end() 반환

s.empty();    // set 비어있으면(원소가 없으면) true
s.size();     // set 원소 개수 반환

s.begin();    // set root node의 iterator(반복자) 반환
s.end();      // set 마지막 node의 다음을 가리키는 iterator(반복자) 반환

s.insert(key);   // set 삽입, 삽입 후 자동 정렬 됨

s.clear();    // set의 모든 원소 제거

s.erase(iter1, iter2); // iter1 ~ iter2가 가리키는 원소까지 제거
s.erase(iter);    // iter가 가리키는 원소 제거 후 정렬
```

- 멤버 함수(`multiset`)

```cpp
#include <set>

multiset<key> ms;

// multiset도 set의 멤버 함수 모두 사용 가능

ms.count(key);   // 해당 key값의 개수(multiset 유용), key가 있는지 확인
```

- 응용(`set`)

```cpp
#include <set>

set<string> s;

s.insert("push");   // 삽입

// 중복 검사할 때 사용
if(s.count(key)==0){
  // 해당 key 존재
}
else{
  // 해당 key 존재 X
}

// 반복자로 순회
// set<string>::iterator iter;
for(auto iter=s.begin(); iter!=s.end(); iter++){
  cout<< iter->first << endl; // 순회
}
```

- 응용(`multiset`)

```cpp
#include <set>

multiset<string, int> ms;

// 반복자로 전체 순회
// set<string>::iterator iter;
for(auto iter=ms.begin(); iter!=ms.end(); iter++){
  cout<< iter->first << endl; // 순회
}

if(ms.count("key") > 1){
  // 해당 key의 value가 2개 이상
}

for(iter = ms.lower_bound(N); iter != ms.upper_bound(N); iter++){
  // Key가 N인 value 값들 조회
  cout << "[" << iter->first << "] " ;
}
```

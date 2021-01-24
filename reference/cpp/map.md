---
title: "C++ map Header"
excerpt: "<map> of C++"
category: Cpp-Reference
tags: [C++, map, multimap]
toc: true
---

## map, multimap of C++

- `#include <map>`

  > Search 용으로 사용(key로 value 검색) vs `<set>`(Only. key만 존재)  
  > (key, value)로 이루어짐.  
  > 중복 불가능: `map`  
  > 중복 가능: `multimap`(`<map>` 에 존재)  
  > 삽입 후 key 값으로 자동 오름차순(디폴트) 정렬

- 생성자(`map`)

```cpp
#include <map>    // 헤더 선언

// map(중복 불가능)
map<key, value> m;      // 기본 map 선언(pair<key, value>로 삽입)
map<key, value> m2(m1);  // m2를 선언(m1을 복사한), =복사생성자
map<key, value, less<key>> m;   // key 값 내림차순 자동 정렬 map 선언
```

- 생성자(`multimap`)

```cpp
#include <map>

// multimap(중복 가능)
multimap<key, value> mm;    // 기본 multimap 선언(pair<key, value>로 삽입)
multimap<key, value, less<key>> mm;  // key 값으로 내림차순 자동 정렬되는 중복 가능 map 선언
```

- 멤버 함수(`map`)

```cpp
#include <map>

map<key, value> m;

m.find(key);    // 해당 key 값과 일치하는 iterator(반복자) 반환, 없다면 m.end() 반환
m.find(key)->second;    // 해당 key 값과 일치하는 value 값 반환

m.empty();    // map이 비어있으면(원소가 없으면) true
m.size();     // map의 원소 개수 반환

m.begin();    // map의 root node의 iterator(반복자) 반환
m.end();      // map의 마지막 node의 다음을 가리키는 iterator(반복자) 반환

m.insert(pair<key, value>);   // map에 삽입, 삽입 후 자동 정렬 됨
m[key]=value;   // 해당 key의 value값 변경, 해당 key 없으면 value값 삽입 후 정렬

m.clear();    // map의 모든 원소 제거

m.erase(iter);    // iter가 가리키는 원소 제거 후 정렬
m.erase(iter1, iter2);      // iter1이 가리키는 원소부터 iter2가 가리키는 원소까지 제거
m.erase(key);     // 해당 key 원소 제거
```

- 멤버 함수(`multimap`)

```cpp
#include <map>

// multimap도 map의 멤버 함수 모두 사용 가능

multimap<key, value> mm;

mm.count(key);   // 해당 key값의 value 개수(multimap에 유용)
```

- 응용(`map`)

```cpp
#include <map>

map<string, int> m;

pair<string, int> p1 = make_pair("key", 5);    // <map> 헤더에 존재

m.insert(p1);   // 삽입
m["push"] = 7;    // (key, value) = ("push", 7) 삽입

// 중복 검사할 때 사용
if(m.find("key") != m.end()){
  // 해당 key 존재
}
else{
  // 해당 key 존재 X
}

// 반복자로 순회
// map<string, int>::iterator iter;
for(auto iter=m.begin(); iter!=m.end(); iter++){
  cout<< iter->first << ", " << iter->second << endl; // 순회
}
```

- 응용(`multimap`)

```cpp
#include <map>

multimap<string, int> mm;

// 반복자로 전체 순회
// map<string, int>::iterator iter;
for(auto iter=mm.begin(); iter!=mm.end(); iter++){
  cout<< iter->first << ", " << iter->second << endl; // 순회
}

if(mm.count("key") > 1){
  // 해당 key의 value가 2개 이상
}

for(iter = mm.lower_bound(N); iter != mm.upper_bound(N); iter++){
  // Key가 N인 value 값들 조회
  cout << "[" << iter->first << ", " << iter->second << "] " ;
}
```

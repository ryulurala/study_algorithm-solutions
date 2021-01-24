---
title: "C++ vector Header"
excerpt: "<vector> of C++"
category: Cpp-Reference
tags: [C++, vector]
toc: true
---

## Vector of C++

- `#include <vector>`

  > for. Array(배열)로 사용  
  > Stack(LIFO 구조)으로 사용 --- for. DFS(깊이 우선 탐색)

- 생성자

```cpp
#include <vector>   // 헤더 선언

vector<T> v;    // T는 Data type. ex) int, string, ...
vector<T> v(n);   // n 개의 0(디폴트값)으로 초기화된 v 선언
vector<T> v(n, elem)  // n 개의 elem 값으로 초기화된 v 선언
vector<T> v2(v1)    // v2 선언(v1을 복사한), =복사생성자
```

- 멤버 함수

```cpp
#include <vector>

vector<T> v;
vector<T> vv;

v.assign(n, elem);  // n 개의 elem 값으로 할당(이전 값을 삭제하고 할당)
v.reserve(n);   // n 개의 위치 예약 --- 미리 동적으로 메모리 할당

v.at(index);    // 해당 index 원소 값 반환 --- 느림, 안전
v[index];   // 해당 index 원소 값 반환 --- 빠름, 불안전

v.front();  // 첫 원소 값 반환(= v[0])
v.back();   // 마지막 원소 값 반환(= v[v.size()-1])

v.begin();  // 첫 원소를 가리키는 iterator(반복자) 반환
v.end();    // 마지막 원소의 다음을 가리키는 iterator(반복자) 반환

v.size();   // 원소 개수 반환
v.capacity();   // capacity(공간) 크기 반환(메모리 크기)

v.empty();    // 비어있으면 true --- capacity(공간) 크기와 상관 X

v.push_back(elem);    // elem 값을 마지막 원소 다음에 삽입 --- 공간 크기는 2배씩 늘어남
v.pop_back();   // 마지막 원소 삭제

v.insert(iter, elem);   // elem 값을 iter가 가리키는 자리에 삽입(해당 자리에 있는 원소부터 뒤로 밀림)
v.insert(iter, n, elem);  // n개의 elem 값을 iter가 가리키는 자리에 삽입(해당 자리에 있는 원소부터 뒤로 밀림)
v.insert(v.end(), vv.begin(), vv.end());    // v 뒤에 vv를 이어 붙임

v.erase(iter);    // 해당 자리의 원소 삭제 --- 해당 자리 다음 원소가 앞으로 당겨짐, 제거한 다음 원소를 가리키는 iterator 반환

v.resize(n);   // n으로 메모리 크기를 변경

v.clear();    // 모든 원소 삭제 --- 공간 크기는 즉시 삭제 X
```

- 응용

```cpp
#include <vector>

vector<int> v;

v.push_back(3);
v.push_back(4);

for(int i=0; i<v.size(); i++){
  v[i]++;
}

// 위와 동일
for(int& elem: v){
  elem++;
}

// 위와 동일
for(auto& elem: v){   // c++ 11부터 가능
  elem++;
}

v.pop_back();
v.pop_back();

vector<vector<int>> vv;       // 2차원 배열

// 4 x 4 배열 만들기
for(int i=0; i<4; i++){
  vector<int> temp(4);
  vv.push_back(temp);
}

vector<pair<int, int>> vp;    // pair는 <vector> 헤더에 들어있어 사용 가능

pair<int, int> p = make_pair(3, 4);
v.push_back(p);

v.push_back(make_pair(5, 6));
```

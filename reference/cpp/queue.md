---
title: "C++ queue Header"
excerpt: "<queue> of C++"
category: Cpp-Reference
tags: [C++, queue, priority_queue]
toc: true
---

## Queue of C++

- `#include <queue>`

  > Queue(FIFO 구조)  
  > for. BFS(너비 우선 탐색)  
  > for. 우선 순위 큐(priority_queue) 사용, **default: top() 값은 큰 값**

- 생성자

```cpp
#include <queue>    // 헤더 선언

// 기본 큐
queue<T> q;   // 기본 T 형 큐 선언
queue<T, list<T>> q;    // List 구조 + 큐 선언(default: deque 구조)

// 우선 순위 큐
priority_queue<T> pq;   // 기본 T형 우선 순위 큐 선언
priority_queue<T, deque<T>> pq;   // deque 구조 + 우선 순위 큐 선언(default: vector 구조)
priority_queue<T, vector<T>, greater<T>> pq;    // vector 구조 + 큰 원소 값이 나중에 나옴(default: less<T>)
```

- 멤버 함수

```cpp
#include <queue>

// 기본 큐
queue<int> q;

q.front();    // 맨 앞 원소 값 반환
q.back();     // 맨 마지막 원소 반환

q.empty();    // 큐가 비어있으면 true

q.size();     // 큐가 들어있는 원소 개수 반환

q.push(elem);   // elem 값 back 에 삽입
q.pop();      // front 원소 삭제(반환되는 값 없음)

// 우선 순위 큐
priority_queue<int> pq;

pq.top();   // 맨 앞 원소 값 반환

pq.push(elem);    // elem 값 삽입
pq.pop();     // top 원소 값 삭제
```

- 응용

```cpp
#include <queue>

queue<int> q;

q.push(3);
q.push(2);
q.push(5);

while(!q.empty()){
  cout << q.front() << endl;      // 순서: 3, 2, 5으로 출력
  q.pop();
}

priority_queue<int, vector<int>, greater<int>> pq;    // 큰 값이 나중에 나오는 우선 순위 큐

pq.push(3);
pq.push(2);
pq.push(5);

while(!pq.empty()){
  cout << pq.top() << endl;   // 순서: 2, 3, 5 출력
  pq.pop();
}

// 큐 모든 원소 삭제
{
  queue<int> qq;
  swap(q, qq);      // q를 clear() 할 때 사용
}

// 중요!!!!!!!!!!!!!!!!!!!!!!!!!! 우선 순위 큐 - 비교 함수 지정
struct cmp{   // second가 큰 것부터, 같으면 first가 큰 것부터
  bool operator()(pair<int, int> p1, pair<int, int> p2){
    if(p1.second == p2.second) return p1.first < p2.first;
    return p1.second < p2.second;
  }
};    // 세미콜론 ';' 필수

priority_queue<pair<int, int>, vector<pair<int, int>>, cmp> pq;   // 비교 기준 변경
```

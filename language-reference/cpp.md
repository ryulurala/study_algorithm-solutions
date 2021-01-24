---
title: "C++ Reference"
excerpt: "C++ Reference"
category: Launguage Reference
tags:
  [
    C++,
    iostream,
    vector,
    algorithm,
    queue,
    string,
    map,
    set,
    multimap,
    multiset,
  ]
toc: true
toc_sticky: true
---

## `#include <iostream>`

- for. 출력(cout, printf 이용)

```cpp
#include <iostream>   // 헤더 선언

// cout
cout << "" << 변수; // 변수 출력(연산자 오버로딩 돼있다)
cout << endl;   // 개행

// printf()도 가능
printf("%c %d %lf %s", char형, int형, double형, '\0' 있는 char*형);

```

---

## `#include <vector>`

- for. Array(배열)로 사용
- Stack(LIFO 구조)으로 사용 --- for. DFS(깊이 우선 탐색)

1. 생성자

```cpp
#include <vector>   // 헤더 선언

vector<T> v;    // T는 Data type. ex) int, string, ...
vector<T> v(n);   // n 개의 0(디폴트값)으로 초기화된 v 선언
vector<T> v(n, elem)  // n 개의 elem 값으로 초기화된 v 선언
vector<T> v2(v1)    // v2 선언(v1을 복사한), =복사생성자

```

2. 멤버 함수

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

3. 응용

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

---

## `#include <map>`

- Search 용으로 사용(key로 value 검색) vs `<set>`(Only. key만 존재)
  - (key, value)로 이루어짐.
  - 중복 불가능: `map`
  - 중복 가능: `multimap`(\<map> 에 존재)
  - 삽입 후 key 값으로 자동 오름차순(디폴트) 정렬

1. 생성자

```cpp
#include <map>    // 헤더 선언

// map(중복 불가능)
map<key, value> m;      // 기본 map 선언(pair<key, value>로 삽입)
map<key, value> m2(m1);  // m2를 선언(m1을 복사한), =복사생성자
map<key, value, greater<key>> m;   // key 값 내림차순 자동 정렬 map 선언

// multimap(중복 가능)
multimap<key, value> mm;    // 기본 multimap 선언(pair<key, value>로 삽입)
multimap<key, value, greater<key>> mm;  // key 값으로 내림차순 자동 정렬되는 중복 가능 map 선언
```

2. 멤버 함수

```cpp
#include <map>

map<key, value> m;

m.find(key);    // 해당 key 값과 일치하는 iterator(반복자) 반환, 없다면 m.end() 반환
m.find(key)->second;    // 해당 key 값과 일치하는 value 값 반환

m.empty();    // map이 비어있으면(원소가 없으면) true

m.size();     // map의 원소 개수 반환

m.begin();    // map의 root node의 iterator(반복자) 반환
m.end();      // map의 마지막 node의 다음을 가리키는 iterator(반복자) 반환

m.insert(pair<key, value>);   // map에 삽입, 삽입 후 자동 정렬됨

m[key]=value;   // 해당 key의 value값 변경, 해당 key 없으면 value값 삽입 후 정렬

m.clear();    // map의 모든 원소 제거

m.erase(iter);    // iter가 가리키는 원소 제거 후 정렬
m.erase(iter1, iter2);      // iter1이 가리키는 원소부터 iter2가 가리키는 원소까지 제거
m.erase(key);     // 해당 key 원소 제거

multimap<key, value> mm;

mm.count(key);   // 해당 key값의 value 개수(multimap에 유용)
```

3. 응용

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

multimap<string, int> mm;

if(mm.count("key") > 1){
  // 해당 key의 value가 2개 이상
}

```

---

## `#include <queue>`

- Queue(FIFO 구조)
- for. BFS(너비 우선 탐색)
- for. 우선 순위 큐(priority_queue) 사용, **default: top() 값은 큰 값**

1. 생성자

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

2. 멤버 함수

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

3. 응용

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

---

## `#include <string>`

- 완전 필수!!
- for. 문자열 사용

1. 생성자

```cpp
#include <string>   // 헤더 선언

using namespace std;    // 필요!

string str;     // 기본 문자열 선언, '+=' 연산자 사용하려면 ""로 초기화
string str(s);    // str를 선언(s를 복사한), =복사생성자
string str(n, c);   // n개의 char형 c문자로 초기화된 str 선언

```

2. 멤버 함수

```cpp
#include <string>

using namespace std;    // 필요!

string str;

str.resize(n, c);   // n개로 크기 조절, 작으면 삭제 / 크면 c로 초기화
str.reserve(n);   // 미리 n 크기로 공간 할당(예약)

str.at(index);    // 해당 index의 문자 값 반환 --- 느림, 안전
str[index];     // 해당 index의 문자 값 반환 --- 빠름, 불안전

str.front();    // 문자열의 맨 앞 문자 반환
str.back();   // 문자열의 맨 뒤 문자 반환

str.begin();    // 문자열의 맨 처음 문자를 가리키는 iterator(반복자) 반환
str.end();      // 문자열의 맨 마지막 문자 다음을 가리킨 iterator(반복자) 반환

str.size();   // 문자열의 길이 반환
str.length();   // 문자열의 길이 반환(권장)
str.capacity();   // 문자열의 공간 크기 반환

str.empty();    // 문자열이 비어있으면 true(문자 값이 비어있을 때)

str.find("string");  // "string"과 일치하는 문자열 있으면 인덱스 반환 / 없으면 string::npos 반환
str.find("string", index);  // index 부터 "string"과 일치하는 문자열 있으면 인덱스 반환 / 없으면 string::npos 반환

str.push_back(c);   // 맨 뒤에 c 문자 값 삽입
str.pop_back();   // 맨 뒤 문자 삭제

str += "string";    // 맨 뒤에 "string" 삽입

str.clear();    // 문자열 안에 모든 문자 값 삭제

str.substr();   // str 전체 문자열 반환
str.substr(index);    // index부터 부분 문자열 반환
str.substr(index, count);     // index부터 count개수 만큼 부분 문자열 반환

str.replace(iter, count, str1);   // iter가 가리키는 원소부터 count 개수만큼 str1으로 바꿈

stoi(str);    // str을 int형으로 바꾼 int형 반환
stoi(str, nullptr, 2);    // str을 int형으로 바꾼 2진수 int형 반환

// 주의! 처음부터 숫자가 아니면 exception 발생
// 주의! 숫자로 바꿀 수 있는 인덱스까지 바꿔줌.

stod(str)   // double형으로
stof(str)   // float형으로
stol(str)   // long형으로

```

1. 응용

```cpp
#include <string>

using namespace std;

string str = "None";
string str1 = "one";

if(str.find(str1) != string::npos){
  // "one"을 찾음
  // 1을 반환(제일 앞 인덱스)
}
else{
  // "one"을 못찾음
}

str.replace(0, 1, "");    // str == "one"
str.replace(str1.find(str1), str1.length(), "two");   // str == "two"

string str2 = str1.substr(1, 2)   // str2 == ne

string str3 = "";   // ""로 꼭! 초기화해줘야 함.
str3 += "string";

```

---

## `#include <algorithm>`

- for. sort(정렬), default: 오름차순

  - sort(): Quick sort
  - stable_sort(): Merge sort
  - sort_heap(): Head sort

- for. 유용한 함수들
  - includes(): 부분 집합 포함 관계
  - reverse(): 뒤집기
  - max() / min(): 최댓값 / 최소값 비교 반환
  - max_element() / min_element(): 최댓값 / 최솟값 원소 값 반환
  - transform() + \<cctype>: 대, 소문자 변환 ++++ 그냥 tolower(char), toupper(char) 이용
  - next_permutation(), prev_permutation(): 순열 + 조합 응용

1. Sort(정렬)

```cpp
#include <algorithm>    // 헤더 선언
#include <vector>

using namepsace std;

vector<int> v;

bool cmp1(int num1, int num2){
  return num1 < num2;  // less<int>와 동일, 오름차순
}

// Quick sort --- 불안정
sort(v.begin(), v.end(), less<int>);  // 작은 것부터, 오름차순

// Merge sort --- 안정(같은 것에 대해 두 번 비교할 때 사용)
stable_sort(v.begin(), v.end(), cmp1);

// Heap sort --- 안정
sort_heap(v.begin(), v.end(), greater<int>);  // 큰 것부터, 내림차순

vector<pair<int, int>> vv;

bool cmp2(pair<int, int> p1, pair<int, int> p2){
  // first가 큰 값이 인덱스가 크다 / first가 같을 경우, second가 큰 값
  if(p1.first == p2.first) return p1.second < p2.second;
  return p1.first < p2.first;
}

stable_sort(vv.begin(), vv.end(), cmp2);  // 정렬

```

2. 유용한 함수들

```cpp
#include <algorithm>    // 헤더 선언
#include <vector>
#include <string>

using namespace std;

string str1 = "abcd";
string str2 = "ad";

bool check = str1.find(str2) == string::npos   // false

// 부분 집합으로 포함 관계를 찾음
check = includes(str1.begin(), str1.end(), str2.begin(), str2.end());   // true

```

<!--
\***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\*** DFS(깊이 우선 탐색) \***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\***

- 실제로 구현할 때는 vector<int> node[N]; 을 선언하고
  // m과 n를 연결할 때는 다음과 같이 한다.
  node[m].push_back(n);
  node[n].push_back(m);

* 2 가지 방법으로 만든다.(재귀 or Stack)

1. node는 전역 변수로 선언
2. 함수의 매개 변수를 참조자로 정의

------- 재귀 구현 -------
ex) 연결된 개수 리턴하는 재귀 DFS
int dfsByRecursive(Node root)
{
if(root.check==true)
{
// TODO 코드(방문 끝남)
return 1; // 개수 하나씩 증가
}

    // 방문 처리
    root.check = true;

    // 원소 개수
    int count = 0;


    for(int i=0; i<root.size(); i++)
    {
      // 인접한 노드를 방문
      count += dfs();
    }
    return count;

}

------- 스택 구현 -------
ex) 연결된 개수 리턴하는 DP DFS
int dfsByStack(Node root)
{
// 원소 개수
int count = 0;

    // 스택 선언
    vector<int> stack;

    // 스택에 시작 값 삽입
    stack.push_back(root);

    // 방문 처리
    root.check = true;

    // DFS 시작
    while(!stack) // 스택에 값이 없을 때까지
    {
      // 스택에 값이 있다면 아직 방문하지 않은 노드가 있다.

      // TODO 코드(방문 끝남)
      count++;
      Node node = stack.back();
      stack.pop_back();

      for(int i=0; i<node.size(); i++)
      { // 방문하지 않았으면 스택에 삽입
        if(node[i].check == false)
        {
          stack.push_back(node[i]); // 다음에 갈 노드
          node[i].check = true;     // 방문 처리
          stack.push_back(node);    // 현재 노드(pop을 했기 때문에 돌아가려면 필요)
          break;
        }
      }
    }

}

\***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\*** BFS(너비 우선 탐색) \***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\***
ex) 연결된 개수 리턴하는 DP BFS
int bfsByQueue(Node root)
{
// 원소 개수
int count = 0;

    // 큐 선언
    queue<int> q;

    // 큐에 시작 값 삽입
    q.push(root);

    // 방문 처리
    root.check = true;

    // BFS 시작
    while(!q.empty())   // 큐에 값이 없을 때까지.
    {
      // 큐에 값이 있다면, 아직 방문하지 않은 노드가 있다.

      // TODO 코드(방문 끝남)
      count++;
      Node node = q.front();
      q.pop();

      // 방문하지 않는 노드 검사
      for(int i=0; i<node.size(); i++)
      {
        // 방문하지 않았으면 큐에 삽입
        if(node[i].check == false)
        {
          q.push(node[i]);
          node[i].check = true;   // 방문 처리
        }
      }
    }
    return count;

}

\***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\*** Union_Find(집합 만들기 알고리즘) \***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\***
vector<int> root; // 각 root
vector<int> rank; // 트리의 높이를 저장
vector<int> nodeCount;

for(int i=0; i<root.size(); i++)
{
root.push_back(i); // root를 자신으로 초기화
rank.push_back(0); // 트리의 높이 초기화
nodeCount.push_back(1) // 노드 개수 초기화
}

int find(int x)
{ // 루트 노드는 부모 노드 번호로 자기 자신을 가진다.
if(x == root[x])
return x;
else // 각 노드의 부모 노드를 찾아 올라간다.
return find(root[x]);
}

int union(int x, int y)
{
x = find(x); // x의 root 찾기
y = find(y); // y의 root 찾기

// 두 값의 root가 같지 않을 때
if(x != y)
{
root[y] = x; // y의 root를 x로 변경
nodeCount[x] += nodeCount[y]; // x의 node 수에 y의 node 수를 더한다.
nodeCount[y] = 1; // y의 node 수는 1로 초기화
}
return nodeCount[x];
}

\***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\*** Algorithm 클래스 \***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\***

- 순열(Permutation)

* 완전 탐색

- 조합

1. 보조 수열로 해당 개수만큼 배열을 만든다.
2. 뽑을 개수만큼 앞에서부터 1을 채운다.
3. prev_permutation을 돌린다.(보조수열의 iterator로)
4. 1로 채워진 곳이 해당 인덱스의 값을 대체하면 된다.

- 멤버 함수

* next_permutation(처음 반복자, 끝 반복자) : 다음 자리를 바꾼다. (sort less 해야됨 = 오름차순으로 바꿔야댐)
* prev_permutation(처음 반복자, 끝 반복자) : 전 자리를 바꾼다. (sort greater 해야됨 = 내림차순으로 바꿔야댐)

ex) 자리를 바꿔가며 조건 검사 예제
do
{
// 조건 검사
}
while(next_permutation(container.begin(), container.end()));

- is_permutation(v1.begin(), v1.end(), v2.begin(), v2.end()) : v2는 v1의 순열인지 확인. bool 값 return

* 중복 있는 합치기

- merge 함수
  ex)
  vector<int> result(v1.size()+v2.size());
  merge(v1.begin(), v1.end(), v2.begin(), v2.end(), result.begin()) : result는 미리 공간을 할당해야하며 중복허용하며 merge한다.

* 중복 없이 합치기
  vector<int> result(v1.size()+v2.size());
  vector<int>::iterator iter;

1. iter = set_union(v1.begin(), v1.end(), v2.begin(), v2.end(), result.begin()) : v1합집합v2
2. iter = set_intersection(v1.begin(), v1.end(), v2.begin(), v2.end(), result.begin()) : v1교집합v2
3. iter = set_difference(v1.begin(), v1.end(), v2.begin(), v2.end(), result.begin()) : v1-v2, 반대로 하려면 v2부터 매개변수를 넣으면 된다.

- result.resize(iter - result.begin()) : 결과의 끝을 return한 iterator이기 때문에 resize해주어야 한다.
- result.erase(iter, result.end()) : iter부터 end()까지 지운다.

* 부분 집합 판별
  vector<int> v1;
  vector<int> v2;
  bool check = includes(v1.begin(), v1.end(), v2.begin(), v2.end());
  if(check == true) : v2는 v1의 부분집합이다. v2 C v1

* 대소문자 변환(for auto 문으로 바꾸려면 참조자를 써야한다.)
  #include <cctype> // ::toupper, ::tolower
  #include <algorithm> // transform
  transform(string.begin(), string.end(), string.begin(), ::toupper); // :: 필수
  transform(string.begin(), string.end(), string.begin(), ::tolower);
  또는

- 소문자가 ASCII 코드 값이 더 크다는 점을 이용하여

1. 소문자 -> 대문자: '문자' -= '소문자'(를) - '대문자'(로);
2. 대문자 -> 소문자: '문자' -= '대문자'(를) - '소문자'(로);

- 거꾸로 뒤집기(<algorithm> 헤더에 있음)
  reverse(str.begin(), str.end()); : string을 거꾸로 뒤집는다.

- min(), max()
  min(const T& a, const T& b): 작은거 리턴
  max(const T& a, const T& b): 큰거 리턴
  ex)
  max(1, 2) -> 2 리턴
  min('b', 'd') -> 'b' 리턴

- min_element(), max_element()
  max_element(vector.begin(), vector.end()): 최대값을 가리키는 반복자 리턴(*max_element(...) 로 최대값을 알 수 있다.)
  min_element(vector.begin(), vector.end()): 최소값을 가리키는 반복자 리턴(*min_element(...) 로 최소값을 알 수 있다.)

\***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\*** 소수 구하기 \***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\***

- 소수 구하기

1. 에라토스테네스의 체: 체로 걸어서 남는 수가 소수이다.
2. 해당 수가 소수인지 판별: 그 수의 root까지 반복문을 돌려 모두 나머지가 0이면 소수이다.

\***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\*** 주의 \***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\***
float, double 등의 부동 소수점 비교는 정확하지 않다.
35.001 != 35.001 인 경우도 있다.
따라서, 부동 소수점의 범위 내에서 전부 곱하여 정수 상태로 비교한다.

\***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\*** 구조체 \***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\***
typedef struct Name{
int a, b, c, d;
Robot(int \_a, int \_b, int \_c, int \_d){ // 생성자
a = \_a;
b = \_b;
c = \_c;
d = \_d;
}
Robot(const Robot& robot){ // 복사 생성자
a = robot.a;
b = robot.b;
c = robot.c;
d = robot.d;
}
bool operator ==(const Robot& robot){ // 비교 연산자 오버로딩
if(a != robot.a) return false;
if(b != robot.b) return false;
if(c != robot.c) return false;
if(d != robot.d) return false;
return true;
}
void operator =(const Robot& robot){ // 대입 연산자 오버로딩
a = robot.a;
b = robot.b;
c = robot.c;
d = robot.d;
}
}Name;

main()
{
Robot robot1(0, 0, 0, 0);
Robot robot2(1, 1, 1, 1);
if(robot1 == robot2){
return 1;
}
return 0;
}

\***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\*** 튜플(tuple)<tuple> \***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\***

- pair 객체는 first, second 두 개만 사용 가능하지만, tuple은 다수의 개가 가능하다.

#include <tuple> 헤더 선언

int main()
{
tuple<int, int, int, int> t; // 튜플 선언
t = make_tuple(1, 2, 3, 4); // make_tuple로 추가

    printf("<before>\n");
    printf("%d\n", get<0>(t));        // 조회, 0, 1, 2, 3은 0부터 시작하는 Index다.
    printf("%d\n", get<1>(t));        // 특정 변수 Index로 조회할 수 없다.
    printf("%d\n", get<2>(t));
    printf("%d\n", get<3>(t));

    get<2>(t) = 10;               // 수정도 가능
    get<3>(t) = 20;

    printf("<after>\n");
    printf("%d\n", get<0>(t));
    printf("%d\n", get<1>(t));
    printf("%d\n", get<2>(t));
    printf("%d\n", get<3>(t));

    return 0;

}

-> 1, 2, 3, 4 출력 후 1, 2, 10, 20이 출력됨.

\***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\*** 중복 가능한 map, set(multimap, multiset) \***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\***
#include <map> // 헤더 선언

multimap<int, int> mm;

for(iter = mm.lower_bound(N); iter != mm.upper_bound(N); iter++){ // Key가 N인 value 값들 조회
cout << "[" << iter->first << ", " << iter->second << "] " ;
}

---

#include <set> // 헤더 선언

multiset<int> ms;

multiset<int>::iterator start, end;

start = ms.lower_bound(N); // 원소 N을 가리키는 처음 위치
end = ms.upper_bound(N); // 원소 N을 가리키는 마지막 위치

\***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\*** 반복자(iterator) \***\*\*\*\*\***\*\*\*\*\***\*\*\*\*\***

일반 순회
for(auto iter = vector.begin(); iter!=vector.end(); iter++){
... 앞에서부터
}

거꾸로 순회
for(auto riter = vector.rbegin(); riter!=vector.rend(); riter++){
... 뒤에서부터
}

---

---

---

---

---

```

``` -->

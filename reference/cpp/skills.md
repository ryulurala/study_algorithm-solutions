---
title: "C++ Skills"
excerpt: "Skills by C++"
category: Cpp-Reference
tags:
  [
    C++,
    <iostream>,
    <algorithm>,
    iterator,
    sort,
    permutation,
    combination,
    dfs,
    bfs,
    brute-force,
    union-find,
    merge,
    set_union,
    set_intersection,
    set_difference,
    lower_bound,
    upper_bound,
    <sstream>,
  ]
toc: true
---

## Skills by C++

### 문자열 추출(sstream)

- `#include <sstream>`

- `stringstream ss(string s)`
  > s를 스트림 버퍼에 넣고 ss를 선언.
- `ss.str(string s)`
  > s를 스트림 버퍼에 넣음.
- `ss.clear()`
  > ss의 스트림 버퍼를 clear.

```cpp
#include <sstream>    // 헤더 필요
#include <string>

using namespace std;

string str1="hi bye 2021 36.5";   // 공백 split은 알아서 sstream이 해줌.
string str2="hi, bye, 2021, 36.5";  // ',' split

// 구분자 split -> 공백 split 으로 바꾼다.
int index=str2.find(',');
while(index!=string::npos){
  str2.replace(index, 1, "");
  index=str2.find(',');
}

// stringstream ss(str2); 아래 두 줄과 같음
stringstream ss;
ss.str(str2);

string hi, bye;
int year;
float temperature;

ss >> hi;   // "hi", string형
ss >> bye;    // "bye", string형
ss >> year;   // 2021, int형
ss >> temperature;    // 36.5, float형

```

### 이진탐색(lower_bound, upper_bound)

- 기본 규칙

  > 정렬돼있어야 함.  
  > 기본적으로 오름차순 정렬

- `lower-bound(begin, end, target)`
  > `<algorithm>` 헤더 필요  
  > `begin` 반복자(iterator)부터 `end` 반복자까지  
  > **`target`값이 있다면**, 가장 작은 `target`값과 일치하는 인덱스를 가리키는 반복자 리턴.  
  > **`target`값이 없다면**, `target`값보다 크지만 가장 작은 값의 인덱스를 가리키는 반복자 리턴.
- `upper-bound(begin, end, target)`
  > `<algorithm>` 헤더 필요  
  > `begin` 반복자(iterator)부터 `end` 반복자까지  
  > **`target`값이 있다면** 가장 큰 `target`값과 일치하는 인덱스를 가리키는 반복자 리턴.  
  > **`target`값이 없다면**, `target`값보다 작지만 가장 큰 값의 인덱스를 가리키는 반복자 리턴.

```cpp
#include <algorithm>  // 헤더 필요
#include <vector>

using namespace std;

vector<int> v;
v.push_back(1);
v.push_back(2);
v.push_back(2);
v.push_back(2);
v.push_back(4);
v.push_back(5);
v.push_back(6);

lower_bound(v.begin(), v.end(), 2) - v.begin();
// 1, target과 같은 값 중 가장 작은 인덱스
v.end() - upper_bound(v.begin(), v.end(), 2);
// 3, target과 같은 값 중 가장 큰 인덱스

lower_bound(v.begin(), v.end(), 3) - v.begin();
// 4, target보다 크지만 가장 작은 인덱스
v.end() - upper_bound(v.begin(), v.end(), 3);
// 3, target보다 작지만 가장 큰 인덱스
```

- 직접 함수 구현

```cpp
#include <vector>

using namespace std;

int lowerBound(vector<int>& vec, int target){
  int left=0;   // 처음
  int right=vec.size();   // 마지막

  while(left<right){
    int mid=(left+right)/2;   // 중간 인덱스

    if(vec[mid]<target) left=mid+1;
    else right=mid;
  }

  return left;  // left
}

int upperBound(vector<int>& vec, int target){
  int left=0;   // 처음
  int right=vec.size();   // 마지막

  while(left<right){
    int mid=(left+right)/2;   // 중간 인덱스

    if(vec[mid]<=target) left=mid+1;  // lowerBound()와 '=' 차이
    else right=mid;
  }

  return right-1;   // right-1
}

vector<int> v;
v.push_back(1);
v.push_back(2);
v.push_back(2);
v.push_back(2);
v.push_back(4);
v.push_back(5);
v.push_back(6);

lowerBound(v, 2); // 1, target과 같은 값 중 가장 작은 인덱스
upperBound(v, 2); // 3, target과 같은 값 중 가장 큰 인덱스

lowerBound(v, 3); // 4, target보다 크지만 가장 작은 인덱스
upperBound(v, 3); // 3, target보다 작지만 가장 큰 인덱스
```

### 출력(cout, printf)

- `#include <iostream>`
- `printf()`
  > 정해진 서식문자로 출력  
  > `printf("%c", char형)`  
  > `printf("%d", int형)`  
  > `printf("%lf", double형)`  
  > `printf("%s", '\0' 있는 char\* 형)`
- `cout`
  > `<<` 연산자가 오버로딩 돼있어 출력하기 편함  
  > `cout<<변수`  
  > `cout<<endl`

```cpp
#include <iostream>   // 헤더 선언

using namespace std;

int main(){
  int num=0;
  // cout
  cout<<""<<num; // 변수 출력(연산자 오버로딩 돼있다)
  cout<<endl;   // 개행

  // printf()도 가능
  printf("%c %d %lf %s", 'a', 36, 36.36, "hihi");
  return 0;
}
```

### 반복자(iterator)

- 일반 순회
  > `begin()`, `end()` 이용

```cpp
  for(auto iter = vector.begin(); iter!=vector.end(); iter++){
    ... 앞에서부터
  }
```

- 거꾸로 순회
  > `rbegin(), rend()` 이용

```cpp
  for(auto riter = vector.rbegin(); riter!=vector.rend(); riter++){
    ... 뒤에서부터
  }
```

### 정렬(sort)

- `#include <algorithm>`

- `sort(.begin(), .end(), compare<T>)`
  > Quick sort  
  > 불안전함
- `stable_sort(.begin(), .end(), compare<T>)`
  > Merge sort  
  > 안전함
- `sort_heap(.begin(), .end(), compare<T>)`

  > Head sort  
  > 안전함

- `compare<T>`

  > `greater<T>`: 오름차순, default  
  > `less<T>`: 내림차순

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

### 부분 집합 판별(includes)

- `#include <algorithm>`
- `includes(parent.begin(), parent.end(), child.begin(), child.end())`
  > 부분집합 포함 관계 확인  
  > child는 parent의 부분집합이면 true, 아니면 false

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

### string, vector 뒤집기(reverse)

- `#include <algorithm>`
- `reverse(.begin(), .end())`
  > `string`, `vector`의 `iterator`를 이용한 뒤집기  
  > `iterator`사용 -> **원본이 바뀐다.**

```cpp
#include <vector>
#include <string>
#include <algorithm>

using namespace std;

string str = "abcd";
vector<int> v;
v.push_back(1);
v.push_back(2);
v.push_back(3);

reverse(str.begin(), str.end());  // "dcba" 원본이 바뀜
reverse(v.begin(), v.end());    // [3, 2, 1] 원본이 바뀜
```

### Max, Min 값 or 요소 찾기

- `#include <algorithm>`

- `max(element1, element2)`, `min(element1, element2)`
  > element1과 element2의 max, min 값을 반환
- `max_element(.begin(), .end())`, `min_element(.begin(), .end())`
  > 해당 컨테이너의 max 요소를 가리키는 iterator 반환

```cpp
#include <vector>
#include <algorithm>

using namespace std;

vector<int> v;

v.push_back(1);
v.push_back(2);
v.push_back(3);
v.push_back(4);
v.push_back(5);

max(1, 3);  // 3
min(2, 4);  // 2

auto maxIter = max_element(v.begin(), v.end());
*maxIter;    // 5
maxIter-v.begin();   // 4  --- index

auto minIter = min_element(v.begin(), v.end());
*minIter;   // 1
minIter-v.begin();  // 0  --- index
```

### 대소문자 변환

- `toupper(char)`, `tolower(char)`

  > char형 문자 하나를 대문자, 소문자로 변환

- `transform(.begin(), end(), ::toupper)`
- `transform(.begin(), end(), ::tolower)`
  > 해당 컨테이너 전체 대소문자 변환  
  > `<algorithm>` 헤더 필요  
  > `::toupper` or `::tolower`은 `<cctype>` 헤더 필요

```cpp
#include <string>
#include <algorithm>  // transform()
#include <cctype>   // ::toupper, ::tolower

using namespace std;

string str="HI hello";

for(char& ch: str){
  ch=toupper(ch);   // "HI HELLO"
}

transform(str.begin(), str.end(), ::tolower);   // "hi hello"
```

### 순열, 조합 구현

- 순열(Permutation) 구현
  > 완전탐색(Brute-force)와 같음  
  > `next_permutation`, `prev_permutation` 으로 구현  
  > 미리 정렬돼있어야 함.  
  > `<algorithm>` 헤더 필요  
  > `next_permutation`: 미리 오름차순 정렬  
  > `prev_permutation`: 미리 내림차순 정렬

```cpp
#include <string>
#include <algorithm>

using namespace std;

string str="12345"; // 반복 횟수: 5P5

stable_sort(str.begin(), str.end(), greater<string>); // 오름차순 정렬
do{
  // 순열 조건
  // 5P5=5! 반복한다.
  // 완전탐색과 같음
  // 오름차순 정렬 -> next_permutation()
}while(next_permutation(str.begin(), str.end()));


stable_sort(str.begin(), str.end(), greater<string>); // 내림차순 정렬
do{
  // 순열 조건
  // 위와 동일, 내림차순 정렬 -> prev_permutation()
}while(prev_permutation(str.begin(), str.end()));
```

- 조합(Combination) 구현
  > `next_permutation`, `prev_permutation` 으로 구현  
  > `<algorithm>` 헤더 필요  
  > 미리 정렬돼있어야 함.  
  > 미리 오름차순 정렬 -> `next_permutation` -> 뽑을 개수 `1`으로 정함  
  > 미리 내림차순 정렬 -> `prev_permutation` -> 뽑을 개수 `0`으로 정함

```cpp
#include <string>
#include <algorithm>

using namespace std;

string str="00111";   // 반복 횟수: 5C2

stable_sort(str.begin(), str.end(), greater<string>); // 오름차순 정렬
do{
  // 조합 조건
  // 5C2 반복한다.
  // 오름차순 정렬 -> next_permuation()
}while(next_permutation(str.begin(), str.end()));


stable_sort(str.begin(), str.end(), greater<string>); // 내림차순 정렬
do{
  // 조합 조건
  // 위와 동일
  // 내림차순 정렬 -> prev_permuation()
}while(prev_permutation(str.begin(), str.end()));
```

### 완전탐색(Brute-Force) 구현

- `next_permutation(.begin(), .end())`
- `prev_permutation(.begin(), .end())`
  > `next_permutation()`: 오름차순 형태를 내림차순 형태까지  
  > `prev_permutation()`: 내림차순 형태를 오름차순 형태까지  
  > `<algorithm>` 헤더 필요
  > +++
- `is_permutation(v1.begin(), v1.end(), v2.begin(), v2.end())`
  > v1의 순열 중 v2가 있는지 확인.  
  > bool 값 return

```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> v;
v.push_back(1);
v.push_back(2);
v.push_back(3);
v.push_back(4);
v.push_back(5);

do{
  // 완전탐색(자리를 바꿔가며 탐색)
  // 5!
  // [1, 2, 3, 4, 5]->[1, 2, 3, 5, 4]-> ... ->[5, 4, 3, 1, 2]->[5, 4, 3, 2, 1]

}while(next_permutation(v.begin(), v.end()));

string str="54321"

do{
  // 완전탐색
  // 5!
  // "54321" -> "54312" -> "54231" -> ... -> "12354" -> "12345"

}while(prev_permutation(str.begin(), str.end()));
```

### DFS(깊이 우선 탐색) 구현

- 초기화(연결)

```cpp
#include <vector>

vector<int> node[N];  // N개의 node형 배열 선언

// m과 n을 연결할 때는 동시에 연결
node[m].push_back(n); // m에 n을 연결
node[n].push_back(m); // n에 m을 연결
```

- Recursive(재귀)로 구현

  > node는 전역 변수로 선언
  > 함수의 매개 변수를 참조자로 정의

```cpp
using namespace std;

typedef struct Node{
  bool check;
  Node(){
    check=false;
  }  // 생성자
}Node;

int dfsByRecursive(Node root){  // 연결된 개수 리턴하는 재귀 DFS
  if(root.check==true){
    // 방문 끝남
    return 1; // 개수 하나씩 증가
  }

  // 방문 처리
  root.check = true;

  // 원소 개수
  int count = 0;

  for(int i=0; i<root.size(); i++){
    // 인접한 노드를 방문
    count += dfsByRecursive(root[i]);
  }
  return count;
}
```

- `Stack` 이용(`vector<T>` 컨테이너)

```cpp
#include <vector>

typedef struct Node{
  bool check;
  Node(){
    check=false;
  }  // 생성자
}Node;

int dfsByStack(Node root){  //  ex) 연결된 개수 리턴하는 DFS
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
    {
      // 방문하지 않았으면 스택에 삽입
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
```

### BFS(너비 우선 탐색) 구현

- `Queue` 이용

```cpp
#include <queue>

typedef struct Node{
  bool check;
  Node(){
    check=false;
  }  // 생성자
}Node;

int bfsByQueue(Node root) // ex) 연결된 개수 리턴하는 BFS
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
```

### Union_Find(집합 만들기)

- `<map>` 컨테이너 이용

```cpp
map<int> root; // 각 root
map<int> rank; // 트리의 높이를 저장
map<int> nodeCount;

for(int i=0; i<root.size(); i++){
  root[i]=i; // root를 자신으로 초기화
  rank[i]=0; // 트리의 높이 초기화
  nodeCount[i]=1; // 노드 개수 초기화
}

int find(int x){ // 루트 노드는 부모 노드 번호로 자기 자신을 가진다.
  if(x == root[x]) return x;
  else return find(root[x]);  // 각 노드의 부모 노드를 찾아 올라간다.
}

int union(int x, int y){
  x = find(x); // x의 root 찾기
  y = find(y); // y의 root 찾기

  if(x != y){   // 두 값의 root가 같지 않을 때
    root[y] = x; // y의 root를 x로 변경
    nodeCount[x] += nodeCount[y]; // x의 node 수에 y의 node 수를 더한다.
    nodeCount[y] = 1; // y의 node 수는 1로 초기화
  }

  return nodeCount[x];
}
```

### 병합, 합집합, 차집합, 교집합

- `merge(v1.begin(), v1.end(), v2.begin(), v2.end(), result.begin())`
  > 중복 허용 합치기  
  > `<algorithm>` 헤더 필요  
  > v1 컨테이너와 v2 컨테이너를 병합하여 result 컨테이너에 할당  
  > result 컨테이너는 미리 공간을 (v1+v2)크기 이상 할당해야 함

```cpp
#include <vector>
#include <algorithm>  // 헤더 필요

using namespace std;

vector<int> v1(5, 1);   // [1, 1, 1, 1 ,1]
vector<int> v2(6, 0);   // [0, 0, 0, 0, 0, 0]
vector<int> result(v1.size()+v2.size());  // size()=11

// [0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1]
// 정렬되어 합쳐짐(+중복 허용)
merge(v1.begin(), v1.end(), v2.begin(), v2.end(), result.begin());
```

- `set_union(v1.begin(), v1.end(), v2.begin(), v2.end(), result.begin())`
  > 중복 없이 합치기(합집합)  
  > `<algorithm>` 헤더 필요  
  > v1과 v2를 합집합 연산으로 result 컨테이너에 할당 후 `iterator` 리턴  
  > v1을 기준으로 합집합 연산  
  > result 컨테이너는 미리 공간을 (v1+v2)크기로 미리 할당 후 resizing  
  > `result.resize(iter-result.begin())`으로 resizing  
  > `result.erase(iter, result.end())`으로 resizing

```cpp
#include <vector>
#include <algorithm>  // 헤더 필요

using namespace std;

vector<int> v1(5, 1);   // [1, 1, 1, 1 ,1]
v1.push_back(0);
v1.push_back(0);  // [1, 1, 1, 1, 1, 0, 0]
vector<int> v2(6, 0);   // [0, 0, 0, 0, 0, 0]
v2.push_back(1);
v2.push_back(1);  // [0, 0, 0, 0, 0, 0, 1, 1]

vector<int> result(v1.size()+v2.size());  // size()=15

// [0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 0, 0]
// v1을 기준으로 합집합(+중복 불가)
// vector<int>::iterator iter
auto iter=set_union(v1.begin(), v1.end(), v2.begin(), v2.end(), result.begin());

// 아래 함수 둘 중 하나로 resizing 필요!!
result.resize(iter-result.begin());   // iter-0 크기로 resize
result.erase(iter, result.end());   // iter 부터 end()까지 지우기
```

- `set_intersection(v1.begin(), v1.end(), v2.begin(), v2.end(), result.begin())`
  > 교집합 구하기  
  > `<algorithm>` 헤더 필요  
  > v1과 v2를 교집합 연산으로 result 컨테이너에 할당 후 `iterator` 리턴  
  > v1을 기준으로 교집합 연산  
  > result 컨테이너는 미리 공간을 (v1 or v2))크기로 미리 할당 후 resizing  
  > `result.resize(iter-result.begin())`으로 resizing  
  > `result.erase(iter, result.end())`으로 resizing

```cpp
#include <vector>
#include <algorithm>  // 헤더 필요

using namespace std;

vector<int> v1(5, 1);   // [1, 1, 1, 1 ,1]
v1.push_back(0);
v1.push_back(0);  // [1, 1, 1, 1, 1, 0, 0]
vector<int> v2(6, 0);   // [0, 0, 0, 0, 0, 0]
v2.push_back(1);
v2.push_back(1);  // [0, 0, 0, 0, 0, 0, 1, 1]

vector<int> result(v1.size()+v2.size());  // size()=15

// [1, 1]
// v1을 기준으로 교집합
// vector<int>::iterator iter
auto iter=set_intersection(v1.begin(), v1.end(), v2.begin(), v2.end(), result.begin());

// 아래 함수 둘 중 하나로 resizing 필요!!
result.resize(iter-result.begin());   // iter-0 크기로 resize
result.erase(iter, result.end());   // iter 부터 end()까지 지우기
```

- `set_difference(v1.begin(), v1.end(), v2.begin(), v2.end(), result.begin())`

  > 차집합 구하기  
  > `<algorithm>` 헤더 필요  
  > v1과 v2를 차집합 연산(`v1-v2`)으로 result에 할당 후 `iterator` 리턴  
  > v1을 기준으로 v2를 차집합 연산  
  > result 컨테이너는 미리 공간을 (v1 or v2))크기로 미리 할당 후 resizing  
  > `result.resize(iter-result.begin())`으로 resizing  
  > `result.erase(iter, result.end())`으로 resizing

```cpp
#include <vector>
#include <algorithm>  // 헤더 필요

using namespace std;

vector<int> v1(5, 1);   // [1, 1, 1, 1 ,1]
v1.push_back(0);
v1.push_back(0);  // [1, 1, 1, 1, 1, 0, 0]
vector<int> v2(6, 0);   // [0, 0, 0, 0, 0, 0]
v2.push_back(1);
v2.push_back(1);  // [0, 0, 0, 0, 0, 0, 1, 1]

vector<int> result(v1.size()+v2.size());  // size()=15

// [1, 1, 1, 0, 0]
// v1을 기준으로 v2를 차집합 연산
// vector<int>::iterator iter
auto iter=set_difference(v1.begin(), v1.end(), v2.begin(), v2.end(), result.begin());

// 아래 함수 둘 중 하나로 resizing 필요!!
result.resize(iter-result.begin());   // iter-0 크기로 resize
result.erase(iter, result.end());   // iter 부터 end()까지 지우기
```

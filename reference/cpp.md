---
title: "C++ Reference"
excerpt: "C++ Reference"
category: Language-Reference
tags: [
    C++,
    <iostream>,
    <algorithm>,
    vector,
    string,
    queue,
    priority_queue
    map,
    set,
    multimap,
    multiset,
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
  > 미리 정렬해야 함. **중요!!**  
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
  > 미리 정렬해야 함. **중요!!**  
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
  > 미리 정렬해야 함. **중요!!**  
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

## String of C++

- `#include <string>`

  > for. 문자열 사용

- 생성자

```cpp
#include <string>   // 헤더 선언

using namespace std;    // 필요!

string str;     // 기본 문자열 선언, '+=' 연산자 사용하려면 ""로 초기화
string str(s);    // str를 선언(s를 복사한), =복사생성자
string str(n, c);   // n개의 char형 c문자로 초기화된 str 선언
```

- 멤버 함수

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

str.replace(index, count, str1);   // index부터 count 개수만큼 str1으로 바꿈

stoi(str);    // str을 int형으로 바꾼 int형 반환
stoi(str, nullptr, 2);    // str을 int형으로 바꾼 2진수 int형 반환

// 주의! 처음부터 숫자가 아니면 exception 발생
// 주의! 숫자로 바꿀 수 있는 인덱스까지 바꿔줌.

stod(str)   // double형으로
stof(str)   // float형으로
stol(str)   // long형으로
```

- 응용

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

for(auto p: m){
  cout<<p.first<<", "<<p.second<<endl;  // 순회
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

for(auto e: s){
  cout<<e<<endl;  // 순회
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

---

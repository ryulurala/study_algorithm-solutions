---
title: "C++ string Header"
excerpt: "<string> of C++"
category: Cpp-Reference
tags: [C++, string]
toc: true
---

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

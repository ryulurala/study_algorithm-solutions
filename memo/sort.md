---
title: "Sort"
excerpt: "about sort"
category: algorithm basic
toc: true
---

## Sort

### 선택 정렬: Selection Sort

- 시간복잡도: `O(N ^ 2)`

- 알고리즘

  - |               오름차순               |              내림차순              |
    | :----------------------------------: | :--------------------------------: |
    | 가장 작은 값을 `선택`해 앞으로 당김. | 가장 큰 값을 `선택`해 앞으로 당김. |
    >

- 소스코드

  ```cpp
  #include <iostream>
  #include <vector>

  using namespace std;

  void swap(int& a, int& b){
      int temp = a;
      a = b;
      b = temp;
  }

  void selection_sort(vector<int>& test){
      // 오름차순 정렬
      for(int i=0; i<test.size(); i++){
          // 현재 index를 최솟값으로 가정
          int min = test[i];
          int index=i;

          // i~size-1 까지 최솟값 index 탐색
          for(int j=i; j<test.size(); j++){
              if(test[j] < min){
                  min = test[j];
                  index = j;
              }
          }

          // Swap
          swap(test[i], test[index]);
      }
  }

  int main(){
      vector<int> test({3, 4, 1, 2, 9, 5, 7, 6, 8, 10});

      selection_sort(test);

      for(int e: test){
          // 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
          cout<<e<<"\n";
      }
  }
  ```

---

### 버블 정렬: Bubble Sort

- 시간복잡도: `O(N ^ 2)`

- 알고리즘

  - |                   오름차순                    |                  내림차순                   |
    | :-------------------------------------------: | :-----------------------------------------: |
    | `인접한 값`과 비교해 작은 값이면 앞으로 당김. | `인접한 값`과 비교해 큰 값이면 앞으로 당김. |

- 소스코드

  ```cpp
  #include <iostream>
  #include <vector>

  using namespace std;

  void swap(int& a, int& b){
      int temp = a;
      a = b;
      b = temp;
  }

  void bubble_sort(vector<int>& test){
      // 오름차순 정렬
      for(int i=0; i<test.size(); i++){

          // 값을 정렬할 집합의 개수가 줄어들면서...
          // test.size()-1, test.size()-2, test.size-3, ...
          for(int j=0; j<test.size()-1-i; j++){
              if(test[j] > test[j+1]){
                  // Swap
                  swap(test[j], test[j+1]);
              }
          }
      }
  }

  int main(){
      vector<int> test({3, 4, 1, 2, 9, 5, 7, 6, 8, 10});

      bubble_sort(test);

      for(int e: test){
          // 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
          cout<<e<<"\n";
      }
  }
  ```

---

### 삽입 정렬: Insertion Sort

- 시간복잡도: `O(N ^ 2)`

- 알고리즘

  - 앞쪽 집합이 정렬돼있다는 가정에서 `적절한 위치에 값을 삽입`한다.
  - 이미 정렬이 돼있는 배열의 집합에 대해서는 아주 빠른 속도의 장점을 가짐.

- 소스코드

  ```cpp
  #include <iostream>
  #include <vector>

  using namespace std;

  void swap(int& a, int& b){
      int temp = a;
      a = b;
      b = temp;
  }

  void insertion_sort(vector<int>& test){
      // 오름차순 정렬
      for(int i=0; i<test.size()-1; i++){
          // 왼쪽 값보다 클 때까지 바꿔줌.
          int j = i;
          while(test[j] > test[j+1]){
              swap(test[j], test[j+1]);
              j--;
          }
      }
  }

  int main(){
      vector<int> test({3, 4, 1, 2, 9, 5, 7, 6, 8, 10});

      insertion_sort(test);

      for(int e: test){
          // 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
          cout<<e<<"\n";
      }
  }
  ```

---

### 퀵 정렬: Quick Sort

- 시간복잡도

  - 평균: `O(N * log(N))`
  - 최악: `O(N ^ 2)`

- 알고리즘

  1. 비균등 분할(pivot보다 작은 집합, pivot보다 큰 집합)
  2. Swap:
     - left와 right 커서가 엇갈릴 경우 큰 값과 pivot 값을 바꿈.
     - 그 외에는 큰 값과 작은 값을 바꿈.
  3. pivot보다 작은 집합, pivot보다 큰 집합에 대해서 재귀적 Quick_sort 실행

- 소스코드

  ```cpp
  #include <iostream>
  #include <vector>

  using namespace std;

  void swap(int& a, int& b){
      int temp = a;
      a = b;
      b = temp;
  }

  void quick_sort(vector<int>& data, int start, int end){
      // 오름차순
      if(start >= end)    // 원소가 1개
          return;

      int pivot = start;  // pivot을 첫 번째 원소로
      int left = start + 1;
      int right = end;

      while(left <= right){
          // 엇갈릴 때까지 반복
          while(data[left] <= data[pivot]){
              // 피벗 값보다 큰 값을 만날 때까지
              left++;
          }

          while(data[right] >= data[pivot] && right > start){
              // 피벗 값보다 작은 값을 만날 때까지
              right--;
          }

          if(left > right){
              // 엇갈릴 경우, 큰 값과 pivot을 바꿈
              swap(data[right], data[pivot]);
          }
          else {
              // 엇갈릴 경우, 큰 값과 작은 값을 바꿈
              swap(data[right], data[left]);
          }
      }

      // recursive, 반으로 나눠서 재실행
      quick_sort(data, start, right-1);
      quick_sort(data, right+1, end);
  }

  int main(){
      vector<int> test({3, 4, 1, 2, 9, 5, 7, 6, 8, 10});

      quick_sort(test, 0, test.size()-1);

      for(int e: test){
          // 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
          cout<<e<<"\n";
      }
  }
  ```

---

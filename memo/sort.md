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

  1. quick_sort()

     - partition()
     - quick_sort() 재호출

       - pivot보다 작은 집합에 대해
       - pivot보다 큰 집합에 대해

  2. partition()

     - 비균등 분할(pivot보다 작은 집합, pivot보다 큰 집합)

     1. left cursor를 피벗 값보다 큰 값을 만날 때까지 반복하며 설정
     2. right cursor를 피벗 값보다 작은 값을 만날 때까지 반복하며 설정
     3. 만약
        - left cursor > right cursor, right cursor의 값과 pivot 값을 swap()
        - left cursor <= right cursor, right cursor의 값과 left cursor의 값을 swap()

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

  int partition(vector<int>& data, int start, int end){
      int pivot = start;
      int left = start+1;
      int right = end;

      while(left <= right){
          // left cursor 이동: pivot의 값보다 클 때까지
          while(left<=end && data[left]<data[pivot]) left++;
          // right cursor 이동: pivot의 값보다 작을 때까지
          while(right>=start && data[right]>data[pivot]) right--;

          if(left < right){
              swap(data[left], data[right]);
          } else {
              swap(data[pivot], data[right]);
              pivot = right;
          }
      }

      return pivot;
  }

  void quick_sort(vector<int>& data, int start, int end){
      if(start >= end)    // 원소가 1개
          return;

      int pivot = partition(data, start, end);

      // pivot 기준으로 나누어 recursive
      quick_sort(data, start, pivot-1);
      quick_sort(data, pivot+1, end);
  }

  int main(){
      vector<int> test({3, 4, 1, 2, 9, 5, 7, 6, 8, 10});

      quick_sort(test, 0, test.size()-1);

      for(int e: test){
          // 1, 2, 3, 4, 5, 6, 7, 8, 9, 10
          cout<<e<<" ";
      }
      cout<<"\n";
  }
  ```

---

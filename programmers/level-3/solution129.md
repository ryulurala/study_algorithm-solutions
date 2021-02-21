---
title: "길 찾기 게임"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-22"
---

## 문제 링크

[길 찾기 게임](https://programmers.co.kr/learn/courses/30/lessons/42892)

### C++

```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

struct Node{
    int x, y, n;
    Node* left;
    Node* right;
    Node(int _x, int _y, int _n){
        x = _x;
        y = _y;
        n = _n;
        left = nullptr;
        right = nullptr;
    }
};

bool cmp(Node a, Node b){
    if(a.y==b.y) return a.x < b.x;  // x는 작은 것부터
    else return a.y > b.y;  // y는 큰 것부터
}

void insert(Node* parent, Node* child){
    if(parent->x > child->x){    // left
        // 자식 존재 여부
        if(parent->left==nullptr) parent->left=child;
        else insert(parent->left, child);
    }
    else{   // right
        // 자식 존재 여부
        if(parent->right==nullptr) parent->right=child;
        else insert(parent->right, child);
    }
}

void order(vector<vector<int> >& v, Node* current){
    v[0].push_back(current->n); // pre_order
    if(current->left!=nullptr) order(v, current->left);
    if(current->right!=nullptr) order(v, current->right);
    v[1].push_back(current->n); // post_order
}

vector<vector<int>> solution(vector<vector<int>> nodeinfo) {
    vector<vector<int>> answer(2);  // for. [0], [1]

    // init
    vector<Node> nodes;
    for(auto vec: nodeinfo){
        int x=vec[0];
        int y=vec[1];
        int n=nodes.size()+1;
        nodes.push_back(Node(x, y, n));
    }
    stable_sort(nodes.begin(), nodes.end(), cmp);   // 정렬

    Node* root=&nodes[0];
    for(int i=1; i<nodes.size(); i++){
        insert(root, &nodes[i]);    // 연결
    }

    // pre, post order
    order(answer, root);

    return answer;
}
```

### JavaScript

```js
function solution(nodeinfo) {
  var answer = [[], []]; // for. [0], [1]

  // struct
  class Node {
    constructor(x, y, n) {
      this.x = x;
      this.y = y;
      this.n = n;
      this.left = null;
      this.right = null;
    }
  }

  const insert = (parent, child) => {
    if (parent.x > child.x) {
      // left
      if (parent.left === null) parent.left = child;
      else insert(parent.left, child);
    } else {
      // right
      if (parent.right === null) parent.right = child;
      else insert(parent.right, child);
    }
  };

  const order = (node) => {
    answer[0].push(node.n); // pre-order
    if (node.left !== null) order(node.left);
    if (node.right !== null) order(node.right);
    answer[1].push(node.n); // post-order
  };

  // init
  const nodes = nodeinfo
    .map((v, i) => {
      const x = v[0];
      const y = v[1];
      const n = i + 1;
      return new Node(x, y, n);
    })
    .sort((a, b) => {
      if (a.y === b.y) return a.x - b.x;
      // x 오름차순
      else return b.y - a.y; // y 내림차순
    });

  // insert
  const root = nodes[0];
  for (let i = 1; i < nodes.length; i++) {
    insert(root, nodes[i]);
  }

  // order(pre, post)
  order(root);

  return answer;
}
```

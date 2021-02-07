---
title: "베스트앨범"
category: 프로그래머스[Level-3]
tags: [C++, JavaScript, 프로그래머스]
date: "2021-02-07"
---

## 문제 링크

[베스트앨범](https://programmers.co.kr/learn/courses/30/lessons/42579)

### C++

```cpp
#include <string>
#include <vector>
#include <map>
#include <algorithm>
#include <iostream>

using namespace std;

bool cmp(pair<int, int> a, pair<int, int> b) {
    return a.second>b.second;
}

vector<int> solution(vector<string> genres, vector<int> plays) {
    vector<int> answer;

    int size=plays.size();

    map<string, int> genres_total;  // 장르_총 플레이 횟수
    map<string, vector<pair<int, int>>> genres_plays; // 장르_[고유번호_플레이횟수]
    for(int i=0; i<size; i++){
        genres_total[genres[i]]+=plays[i];
        genres_plays[genres[i]].push_back(make_pair(i, plays[i]));
    }

    vector<pair<int, string>> plays_genres; // 플레이 횟수_장르
    for(auto e: genres_total) plays_genres.push_back(make_pair(e.second, e.first));
    stable_sort(plays_genres.rbegin(), plays_genres.rend());  // 장르 횟수 내림차순 정렬

    for(auto e1: plays_genres){
        string genre=e1.second;
        int count=0;
        stable_sort(genres_plays[genre].begin(), genres_plays[genre].end(), cmp);
        for(auto e2: genres_plays[genre]){
            if(count==2) break;
            int number=e2.first;
            answer.push_back(number);
            count++;
        }
    }

    return answer;
}
```

### JavaScript

```js
function solution(genres, plays) {
  var answer = [];

  const len = genres.length;
  const genres_total = {}; // 장르당 총 플레이 횟수
  const genre_id_play = {}; // 장르당 고유 번호_플레이 횟수
  for (let i = 0; i < len; i++) {
    if (genres_total[genres[i]]) {
      // 장르 key 있을 때
      genres_total[genres[i]] += plays[i]; // 총 갯수
      genre_id_play[genres[i]].push([i, plays[i]]); // push
    } else {
      // 해당 장르 없을 때
      genres_total[genres[i]] = plays[i];
      genre_id_play[genres[i]] = [[i, plays[i]]];
    }
  }

  // 총 횟수 내림차순 정렬
  const genres_plays = [];
  for (const key in genres_total) genres_plays.push([key, genres_total[key]]);
  genres_plays.sort((a, b) => b[1] - a[1]);

  // push
  genres_plays.forEach((v) => {
    const topGenre = v[0];
    const id_play = genre_id_play[topGenre];
    id_play.sort((a, b) => b[1] - a[1]); // 플레이 횟수 내림차순
    answer.push(...id_play.slice(0, 2).map((v) => v[0])); // 2개까지 고유번호 push
  });

  return answer;
}
```

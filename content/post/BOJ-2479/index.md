---
title: "BOJ 2479"
description: "경로 찾기"
date: 2022-05-02T09:05:51+09:00
image:

slug: 

categories:
    - "Problem Solving"
    - "KOI"
  
tags:
    - "Study"
    - "Algorithm"
    - "BFS"
    - "Map"

math: true
hidden: false
comments: false
draft: false
---

## BOJ 2470 경로 찾기

[link](https://boj.kr/2479)

### 문제

하나의 이진 코드에서 시작한다. 1자리의 비트만 바꾸는 연산을 최소로 해서 주어진 최종 이진 코드를 구하면 된다.  

### 풀이

시작하는 이진 코드에서 한자리씩 바꿔가며 map에 있는지, 더 짧은 거리가 없는지 조사한다. 조건을 만족하면 큐에 넣고 다시 반복한다.  
간단한 BFS다.

### 소스코드

> [C++](https://github.com/Kadrick/PS/blob/main/BOJ/2479.cpp)

```cpp
/**
 * @file 2479.cpp
 * @author Kadrick (kbk2581553@gmail.com)
 * @brief map
 * @version 0.1
 * @date 2022-04-29 10:38
 *
 * @copyright Copyright (c) 2022
 *
 */
#include <bits/stdc++.h>
using namespace std;
#define fastio                 \
  ios::sync_with_stdio(false); \
  cin.tie(0);
#define endl '\n'

int main(void)
{
  fastio;

  int n, k, start, end;
  cin >> n >> k;

  vector<int> parent(n + 1, -1);
  vector<string> bucket(n + 1, "");

  unordered_map<string, int> table;

  for (int i = 0; i < n; i++)
  {
    string input;
    cin >> input;
    table[input] = i + 1;
    bucket[i + 1] = input;
  }

  cin >> start >> end;

  queue<pair<string, int>> q;
  q.push({bucket[start], start});

  while (!q.empty())
  {
    auto front = q.front();
    q.pop();

    if (front.first == bucket[end])
      break;

    for (int i = 0; i < k; i++)
    {
      string trans = front.first;
      trans[i] = (trans[i] == '0' ? '1' : '0');

      auto pos = table.find(trans);
      if (pos == table.end() || parent[(*pos).second] != -1 || (*pos).second == start)
        continue;

      parent[(*pos).second] = front.second;
      q.push({trans, (*pos).second});
    }
  }

  if (parent[end] == -1)
    cout << -1 << endl;
  else
  {
    vector<int> ans;
    ans.push_back(end);
    end = parent[end];

    while (end != -1)
    {
      ans.push_back(end);
      end = parent[end];
    }

    for (int i = ans.size() - 1; i >= 0; i--)
      cout << ans[i] << ' ';
    cout << endl;
  }

  return 0;
}
```

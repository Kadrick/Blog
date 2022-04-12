---
title: "BOJ 21924"
description: "도시 건설"
date: 2022-04-12T13:07:11+09:00
image: "boj-banner.png"

slug: 

categories:
    - "Problem Solving"

tags:
    - "Study"
    - "Algorithm"
    - "MST" 
    - "Kruskal"

hidden: false
comments: false
draft: false
---

## BOJ 21924 도시 건설

[link](https://boj.kr/21924)

### 문제

요약하면 (그래프에 속하는 모든 간선의 가중치의 합 - MST에 속하는 간선의 가중치의 합)을 구하는 문제다.

### 풀이

MST를 구하는 문제와 다를 것이 없다.
Kruskal 알고리즘을 사용해서 문제를 풀었다.

### 소스코드 

> [C++](https://github.com/Kadrick/PS/blob/main/BOJ/21924.cpp)
```cpp
/**
 * @file 21924.cpp
 * @author Kadrick (kbk2581553@gmail.com)
 * @brief MST
 * @version 0.1
 * @date 2022-04-12 12:55
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

int n, m;
long long total;
vector<int> parent;
vector<pair<int, pair<int, int>>> edges;

int find(int root)
{
  if (root == parent[root])
    return root;
  return parent[root] = find(parent[root]);
}

bool merge(int u, int v)
{
  u = find(u);
  v = find(v);

  if (u == v)
    return false;

  if (u > v)
    swap(u, v);

  parent[v] = u;
  return true;
}

int main(void)
{
  fastio;

  cin >> n >> m;
  parent.resize(n + 1);

  for (int i = 0; i <= n; i++)
    parent[i] = i;

  for (int i = 0; i < m; i++)
  {
    int u, v, c;
    cin >> u >> v >> c;
    total += c;

    edges.push_back({c, {u, v}});
  }

  sort(edges.begin(), edges.end());

  int cnt = 0;
  long long mst = 0;
  for (int i = 0; i < m; i++)
  {
    if (merge(edges[i].second.first, edges[i].second.second))
    {
      cnt++;
      mst += edges[i].first;
    }

    if (cnt == n - 1)
      break;
  }

  if (cnt == n - 1)
    cout << total - mst << endl;
  else
    cout << -1 << endl;

  return 0;
}
```
---
title: "BOJ 1162"
description: "도로포장"
date: 2022-04-13T13:28:41+09:00
image: "boj-banner.png"

slug: 

categories:
    - "Problem Solving"

tags:
    - "Study"
    - "Algorithm"
    - "dijkstra"

math: true
hidden: false
comments: false
draft: false
---

## BOJ 1162 도로포장

[link](https://boj.kr/1162)

### 문제

k개의 간선을 무시하고 넘어갈 수 있을 때 도착지까지의 최소비용을 구하는 문제

### 풀이

[BOJ-10217](https://www.acmicpc.net/problem/10217) 과 비슷하게 문제를 풀었다.
10217번은 비용이라는 요소가 추가되었고 이번 문제에서는 비용을 0으로 만드는 횟수가 주어진 것이다.

결국 출발지점(1번노드)에서 도착지점(N번 노드)까지의 최단거리를 구하는 것과 같다. 도로의 이동시간은 자연수라고 하였으니 다익스트라를 써도 된다.
그렇기에 다익스트라를 통해 구하자. 그런데 그냥 다익스트라를 사용하기에는 비용이 0인 간선의 처리가 부족하다. 어떤 간선의 비용을 0으로 만들면 될까? 

어차피 모르니까 전부 다 계산해보자. 왜? k가 20 이하의 자연수다. 기회가 그렇게 많지 않다고 생각된다.
그럼 어떤 간선을 지날 때 기회를 사용해야 하지? 라는 생각이 들 수 있는데 이 문제는 기회를 어디서 쓰는지 묻고 있지 않다. 어쨌든 최소비용을 구하는 문제다.
어디에보다는 몇 번 사용했는지 기록해서 다음과 같이 dist 배열을 만들자.

> ***dist[i][j] = 기회를 j번 사용하여 i번에 도달하였을 때 최소비용***

이러면 결국 정답은 dist[n][0] ~ dist[n][k] 사이의 최솟값이 된다.

다익스트라 과정 중에 새로운 정점을 큐에 넣을 때, (정점까지의 비용, 정점, 기회 소진 횟수)를 같이 넣어서 구현하면 된다.

주의할 점은 입력이 양방향 도로이고, 과정 중 int범위를 넘을 수 있다.

### 소스코드 

> [C++](https://github.com/Kadrick/PS/blob/main/BOJ/1162.cpp)
```cpp
/**
 * @file 1162.cpp
 * @author Kadrick (kbk2581553@gmail.com)
 * @brief dijkstra
 * @version 0.1
 * @date 2022-04-13 12:54
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

#define int long long
const int INF = LLONG_MAX;

int n, m, k, ans = INF;
vector<pair<int, int>> graph[10001];
vector<vector<int>> dist(10001, vector<int>(21, INF));

int32_t main(void)
{
  fastio;

  cin >> n >> m >> k;

  for (int i = 0; i < m; i++)
  {
    int u, v, c;
    cin >> u >> v >> c;
    graph[u].push_back({v, c});
    graph[v].push_back({u, c});
  }

  for (int i = 0; i < 21; i++)
    dist[1][i] = true;
  
  priority_queue<pair<int, pair<int, int>>> pq;
  pq.push({0, {1, 0}});

  while (pq.size())
  {
    int cost = -pq.top().first;
    int here = pq.top().second.first;
    int fix = pq.top().second.second;
    pq.pop();

    if (dist[here][fix] < cost || here == n)
      continue;

    for (auto &&there : graph[here])
    {
      // fix
      if (fix < k && dist[there.first][fix + 1] > cost)
      {
        dist[there.first][fix + 1] = cost;
        pq.push({-cost, {there.first, fix + 1}});
      }
      // no fix
      if (dist[there.first][fix] > cost + there.second)
      {
        dist[there.first][fix] = cost + there.second;
        pq.push({-(cost + there.second), {there.first, fix}});
      }
    }
  }

  for (int i = 0; i < 21; i++)
    ans = min(ans, dist[n][i]);

  cout << ans << endl;

  return 0;
}
```
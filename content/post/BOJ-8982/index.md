---
title: "BOJ 8982"
description: "수족관 1"
date: 2022-05-17T09:38:46+09:00
image:

slug: 

categories:
    - "Problem Solving"
    - "KOI"

tags:
    - "Study"
    - "Algorithm"
    - "Simulation"

math: true
hidden: false
comments: false
draft: false
---

## BOJ 8982 수족관 1

[link](https://boj.kr/8982)

### 문제

물이 수조에서 빠질 때, 수조의 모양과 수조 내의 구멍에 따라 수조에 남는 물의 양이 달라진다.
수조의 모양과 수조 내의 구멍 위치가 주어지면 그에 따라 수조에 남아 있는 물의 양을 계산하자.

### 풀이

풀이 아이디어는 간단하다. 구멍이 있으면 결국 구멍의 위치가 수면의 위치가 된다.
그래서 모든 구멍을 하나씩 보면서 구멍의 위치에 따라 수면을 정해주고 모두 탐색하였다면, 수면의 위치가 바닥의 위치보다 높다면 계산에 포함한다.

### 소스코드

> [C++](https://github.com/Kadrick/PS/blob/main/BOJ/8982.cpp)

```cpp
/**
 * @file 8982.cpp
 * @author Kadrick (kbk2581553@gmail.com)
 * @brief map
 * @version 0.1
 * @date 2022-05-04 09:04
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

#define Bottom pair<pair<int, int>, pair<int, int>>

int n, k, tmp, ans;
map<Bottom, int> sink;
vector<int> hole, up, down, width;

int main(void)
{
  fastio;

  cin >> n;
  cin >> tmp >> tmp;

  int size = (n - 2) / 2;
  up.resize(size, 0);
  down.resize(size, 0);
  width.resize(size, 0);

  for (int i = 0; i < size; i++)
  {
    pair<int, int> lpos, rpos;
    cin >> lpos.first >> lpos.second >> rpos.first >> rpos.second;
    sink[{lpos, rpos}] = i;
    down[i] = lpos.second;
    width[i] = rpos.first - lpos.first;
  }
  cin >> tmp >> tmp;

  cin >> k;
  for (int i = 0; i < k; i++)
  {
    pair<int, int> lpos, rpos;
    cin >> lpos.first >> lpos.second >> rpos.first >> rpos.second;
    hole.push_back(sink[{lpos, rpos}]);
  }

  // update
  for (int i = 0; i < k; i++)
  {
    int ceiling = down[hole[i]];
    // left
    for (int j = hole[i] - 1; j >= 0; j--)
    {
      ceiling = min(ceiling, down[j]);
      up[j] = max(up[j], ceiling);
    }

    ceiling = down[hole[i]];
    // right
    for (int j = hole[i]; j < size; j++)
    {
      ceiling = min(ceiling, down[j]);
      up[j] = max(up[j], ceiling);
    }
  }

  for (int i = 0; i < size; i++)
  {
    if (up[i] < down[i])
      ans += (down[i] - up[i]) * width[i];
  }

  cout << ans << endl;

  return 0;
}
```

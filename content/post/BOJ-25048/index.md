---
title: "BOJ 25048"
description: "랜선 연결"
date: 2022-05-17T09:38:30+09:00
image:

slug: 

categories:
    - "Problem Solving"
    - "2022 DGIST 현풍전산배 알고리즘 대회"

tags:
    - "Study"
    - "Algorithm"
    - "DP"

math: true
hidden: false
comments: false
draft: false
---

## BOJ 25048 랜선 연결

[link](https://boj.kr/25048)

### 문제

$N$ 개의 스위치를 이용해 $M$ 개의 컴퓨터에 인터넷 공급을 한다.
스위치는 $a_i$ 개의 포트가 있고 $b_i$ 의 설치비용이 발생한다.
스위치끼리 사이클이 없고, 남는 포트가 없으며, 최소 비용으로 연결하는게 목적이다.
가능하면 최소비용 출력, 아니면 -1을 출력한다.

### 풀이

스위치의 하나의 포트엔 반드시 인터넷이 들어가야 한다.
그러면 남은 포트를 생각해보자. 남은 포트엔 스위치 혹은 컴퓨터가 자리 잡는다. 나눠서 생각해보자.

* 스위치가 연결되면 -> (하나의 포트엔 인터넷, 남은 자리는 스위치 혹은 컴퓨터...)
* 컴퓨터가 연결되면 -> 연결할 컴퓨터가 줄어든다.

스위치가 연결되면 같은 문제가 반복된다. 컴퓨터가 연결되면 연결할 컴퓨터의 수가 줄어든다.
여기서 dp로 풀 수 있겠구나 싶었다.

> ***DP[i] = i개의 컴퓨터를 설치했을 때 최소 비용***

각 스위치는 인터넷 포트를 제외한 모든 포트에 컴퓨터가 연결된 것이 기저 사례이고, 하나씩 스위치로 바꿔보는 것만 구현하면 문제가 쉽게 풀린다.
스위치를 꼽는 건 부분 문제니까 스위치를 안 꼽으면 부분문제가 없으니 기저 사례가 된다.

### 소스코드

> [C++](https://github.com/Kadrick/PS/blob/main/BOJ/25048.cpp)

```cpp
/**
 * @file 25048.cpp
 * @author Kadrick (kbk2581553@gmail.com)
 * @brief DP
 * @version 0.1
 * @date 2022-05-03 15:35
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

int n, m;
vector<int> netswitch, cost;
vector<int> dp;

int32_t main(void)
{
  fastio;

  cin >> n;
  netswitch.resize(n);
  cost.resize(n);

  for (int i = 0; i < n; i++)
    cin >> netswitch[i] >> cost[i];

  cin >> m;

  if (m == 1)
    cout << 0 << endl;
  else
  {
    dp.resize(m + 1, LLONG_MAX);

    // dp[n] = n개의 컴퓨터를 설치할 때 최소 비용
    dp[0] = 0;

    for (int i = 0; i < n; i++)
    {
      // 하나는 인터넷 하나는 다른 공유기 나머지 컴퓨터라고 생각
      for (int j = m - (netswitch[i] - 2); j >= 1; j--)
      {
        // 깔끔한 연결이 아님
        if (dp[j] == LLONG_MAX)
          continue;

        // 최소 비용 연결
        dp[j + (netswitch[i] - 2)] = min(dp[j + (netswitch[i] - 2)], dp[j] + cost[i]);
      }

      // 다른 스위치를 꼽지 않고 인터넷과 컴퓨터만 연결되어 있는 경우
      if (netswitch[i] - 1 <= m)
        dp[netswitch[i] - 1] = min(dp[netswitch[i] - 1], cost[i]);
    }

    cout << (dp[m] == LLONG_MAX ? -1 : dp[m]) << endl;
  }

  return 0;
}
```

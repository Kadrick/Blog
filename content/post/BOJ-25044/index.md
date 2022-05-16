---
title: "BOJ 25044"
description: "에어컨"
date: 2022-05-16T11:18:28+09:00
image: "boj-banner.png"

slug: 

categories:
    - "Problem Solving"
    - "2022 DGIST 현풍전산배 알고리즘 대회"

tags:
    - "Study"
    - "Algorithm"
    - "Simulation"

math: true
hidden: false
comments: false
draft: true
---

## BOJ 25044 에어컨

[link](https://boj.kr/25044)

### 문제

에어컨은 정기적으로 3번 멈춘다. 그런데 에어컨 내장시계가 고장나서 3번 꺼지면 시계가 멈췄다 다시 돌아간다.
현실시간으로 N일째의 에어컨이 꺼지는 시각을 구하는 문제이다.

### 풀이

결국 내장시계는 0시에서 15시간 -> 3시간 -> 3시간 -> k분 -> 3시간 루틴으로 하루를 지낸다. 분 계산을 시간 계산으로 하면 소수가 되니까 모든 시간을 분으로 바꿨다.
그리고 N일 때의 범위를 정했다. 내장시계가 아닌 현실 시계가 N일 때는 언제부터이고 (N + 1)일은 언제까지인지를 미리 계산한다.
이후 지정된 루틴을 그대로 수행하면서 N일 때 범위 안에 들어가는 경우를 검사해준다.

평소와 다르게 printf를 썼는데 format 때문에 그랬다. C++20 에서는 std::format 이라는게 생겼다고 하는데 기회가 되면 사용해보자.

### 소스코드

> [C++](https://github.com/Kadrick/PS/blob/main/BOJ/25044.cpp)

```cpp
/**
 * @file 25044.cpp
 * @author Kadrick (kbk2581553@gmail.com)
 * @brief  implement
 * @version 0.1
 * @date 2022-05-03 10:23
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

int n, k, idx, cur;
int add[5] = {15 * 60, 3 * 60, 3 * 60, 0, 3 * 60};
vector<int> ans;

void print(int min)
{
  printf("%02d:%02d\n", min / 60, min % 60);
}

int main(void)
{
  // fastio;

  scanf("%d %d", &n, &k);

  add[3] = k;
  int left = 24 * 60 * n;
  int right = 24 * 60 * (n + 1);

  // simulate
  while (cur + add[idx] < right)
  {
    cur += add[idx];
    if (left <= cur && idx < 3)
      ans.push_back(cur);

    idx += 1;
    idx %= 5;
  }

  cout << ans.size() << endl;
  for (auto &&time : ans)
    print(time - left);

  return 0;
}
```

---
title: "BOJ 2672"
description: "여러 직사각형의 전체 면적 구하기"
date: 2022-05-04T13:06:58+09:00
image: "boj-banner.png"

slug: 

categories:
    - "Problem Solving"
    - "KOI"

tags:
    - "Study"
    - "Algorithm"
    - "Sweeping"

math: true
hidden: false
comments: false
draft: true
---

## BOJ 2672 여러 직사각형의 전체 면적 구하기

[link](https://boj.kr/2672)

### 문제

여러 개의 직사각형이 차지하는 면적을 구하는 문제이다.

### 풀이



### 소스코드

> [C++](https://github.com/Kadrick/PS/blob/main/BOJ/2672.cpp)

```cpp
/**
 * @file 2672.cpp
 * @author Kadrick (kbk2581553@gmail.com)
 * @brief sweeping
 * @version 0.1
 * @date 2022-05-03 09:11
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

typedef struct _RECT
{
  int x, open;     // x pos, open or close
  int bottom, top; // y pos
} Rect;

bool comp(const Rect &left, const Rect &right)
{
  if (left.x == right.x)
    return left.open < right.open;
  return left.x < right.x;
}

int n, mask[20001];
vector<Rect> pool;

int main(void)
{
  fastio;

  cin >> n;
  for (int i = 0; i < n; i++)
  {
    double x, y, w, h;
    cin >> x >> y >> w >> h;

    x *= 10;
    y *= 10;
    w *= 10;
    h *= 10;

    Rect left, right;
    left.open = 1;
    right.open = -1;

    left.x = x;
    right.x = x + w;

    left.bottom = y;
    left.top = y + h;

    right.bottom = y;
    right.top = y + h;

    pool.push_back(left);
    pool.push_back(right);
  }

  sort(pool.begin(), pool.end(), comp);

  long long ans = 0;
  int before = 0;

  for (auto &&line : pool)
  {
    // calc
    int height = 0;
    for (int i = 0; i < 20001; i++)
      if (mask[i])
        height++;

    ans += height * (line.x - before);

    // update
    for (int i = line.bottom + 1; i <= line.top; i++)
      mask[i] += line.open;
    before = line.x;
  }

  if (ans % 100)
  {
    cout << fixed;
    cout.precision(2);
    cout << ans / 100.0 << endl;
  }
  else
    cout << ans / 100 << endl;

  return 0;
}
```

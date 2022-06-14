---
title: "BOJ 25045"
description: "비즈마켓"
date: 2022-05-17T09:36:09+09:00
image:

slug: 

categories:
    - "Problem Solving"
    - "2022 DGIST 현풍전산배 알고리즘 대회"

tags:
    - "Study"
    - "Algorithm"
    - "Greedy"
    - "Sorting"

math: true
hidden: false
comments: false
draft: false
---

## BOJ 25045 비즈마켓

[link](https://boj.kr/25045)

### 문제

상품들은 만족도를 고객들은 지불하고자 하는 비용을 각각 가지고 있다. 고객 만족도가 (만족도 - 비용) 일때 고객 만족도의 합의 최댓값을 구하자.

### 풀이

항상 고객 만족도를 최대로 하는 고객에게 물건을 팔면 된다.

### 소스코드

> [C++](https://github.com/Kadrick/PS/blob/main/BOJ/25045.cpp)

```cpp
/**
 * @file 25045.cpp
 * @author Kadrick (kbk2581553@gmail.com)
 * @brief sort
 * @version 0.1
 * @date 2022-05-03 13:38
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

int n, m, ans;
vector<int> product, company;

int32_t main(void)
{
  fastio;

  cin >> n >> m;

  product.resize(n);
  company.resize(m);

  for (int i = 0; i < n; i++)
    cin >> product[i];

  for (int i = 0; i < m; i++)
    cin >> company[i];

  sort(product.begin(), product.end(), greater<int>());
  sort(company.begin(), company.end());

  for (int i = 0; i < min(n, m); i++)
    ans += max(0ll, product[i] - company[i]);

  cout << ans << endl;

  return 0;
}
```

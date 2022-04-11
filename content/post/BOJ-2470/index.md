---
title: "BOJ 2470"
description: "두 용액"
date: 2022-04-11T21:06:22+09:00
image: "boj-banner.png"

slug: 

categories:
    - "Problem Solving"

tags:
    - "Study"
    - "Algorithm"
    - "two pointers"

math: true
hidden: false
comments: false
draft: false
---
## BOJ 2470 두 용액

[link](https://boj.kr/2470)

### 문제

요약하면 주어진 배열에서 두 수를 더했을 때 0에 가장 가까운 두 수를 구하는 것이다. 

### 풀이

Two pointers 알고리즘을 알고 있다면, 쉽게 풀 수 있다.

풀이는 다음과 같다.

left가 배열의 처음 / right가 배열의 마지막을 가르치고 있다.

1. 우선 들어온 용액을 오름차순 정렬한다.
2. left가 가리키는 수와 right가 가리키는 수를 더한다.  
   2-1. 더한 결과가 현재 0과 가까운 수보다 더 0에 가까우면 업데이트한다. 결과가 0이라면 그대로 종료해도 된다.   
   2-2. 더한 결과가 0보다 작다면 left를 +1 해준다. 이후 다시 2번부터 진행한다.
   2-3. 더한 결과가 0보다 크다면 right를 -1 해준다. 이후 다시 2번부터 진행한다.

반복하다가 left < right 를 만족하지 못하면 종료한다.

두 수의 합에 따라 용액을 더 넣거나 빼는 것으로 생각하면 쉽다.

### 소스코드 

> [C++](https://github.com/Kadrick/PS/blob/main/BOJ/2470.cpp)
```cpp
/**
 * @file 2470.cpp
 * @author Kadrick (kbk2581553@gmail.com)
 * @brief two pointers
 * @version 0.1
 * @date 2022-04-11 20:53
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

void solve(int n, vector<int> &water)
{
  pair<int, int> ans;
  int left = 0, right = n - 1;
  ans.first = ans.second = 1e9;
  while (left < right)
  {
    if (abs(water[left] + water[right]) <= abs(ans.first + ans.second))
    {
      ans.first = water[left];
      ans.second = water[right];

      if (ans.first + ans.second == 0)
        break;
    }

    if (water[left] + water[right] < 0)
      left++;
    else
      right--;
  }

  cout << ans.first << ' ' << ans.second << endl;
}

int main(void)
{
  fastio;

  int n;
  vector<int> water;
  cin >> n;
  water.resize(n);
  for (int i = 0; i < n; i++)
    cin >> water[i];

  sort(water.begin(), water.end());
  solve(n, water);

  return 0;
}
```

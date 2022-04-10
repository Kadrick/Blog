---
title: "TestPost"
description: 
date: 2022-04-10T12:53:11+09:00
image: 
math: 
license: 
hidden: false
comments: true
draft: false
---

Test

```go
/**
 * @file 1069.go
 * @author kadrick (kbk2581553@gmail.com)
 * @brief math
 * @version 0.1
 * @date 2022-04-06 11:11
 *
 * @copyright Copyright (c) 2021
 *
 */
package main

import (
	"fmt"
	"math"
)

func min(a, b float64) float64 {
	if a < b {
		return a
	}
	return b
}

func main() {
	var x, y, d, t float64
	fmt.Scan(&x, &y, &d, &t)

	dist, ans := math.Sqrt(x*x+y*y), 0.0

	// case1: just walk
	ans = dist
	jump := math.Floor(dist / d)

	left := dist - jump*d

	// case2: jump + walk
	ans = min(ans, jump*t+left)
	// case3: jump + 1
	if jump > 0 {
		ans = min(ans, (jump+1)*t)
	}
	// case4: 2jumps
	if jump == 0 {
		ans = min(ans, 2*t)
	}
	// case5: overjump + walk
	ans = min(ans, (jump+1)*t+d-left)

	fmt.Println(ans)
	return
}
```
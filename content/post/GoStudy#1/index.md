---
title: "GoStudy#1"
description: "Golang 첫번째 이야기"
date: 2022-04-11T09:24:17+09:00
image: 
categories:
    - "Go Study"

tags:
    - "Study"
    - "Language"
    - "Go"

hidden: false
comments: false
draft: false
---

# Go?

## 나는 왜 사용하는가
회사에서 Go 를 쓰게 될 것 같다고 해서 며칠간 Go를 이용해 문제를 풀었었다. 언어에 익숙해지는 것도 문제 풀이만큼 좋은 건 없다고 생각해서...  

실제 개발은 아니었지만, 며칠간의 문제 풀이에서 배우고 느낀 것을 정리해보자면...

* Java와 가깝다.  
  문제 풀이하면서 가장 크게 생각한 점이다. 
  Java 처럼 패키지를 이용해야 하기도 하지만, C++ 처럼 포인터를 사용할 수 있다.
  사실 그냥 package가 있는 것부터 Java에 가깝다고 생각한다. 자세히는 모르겠다. 아직 실제 개발을 안 해봐서...
* STL이 없다. 그런데, map이랑 vector가 공짜?  
  처음 하는 처지에서 slice 문법과 Heap package는 나한테 너무 가혹했다. 사실 이건 내가 C++ 로 PS를 했었기 때문에 너무 익숙해져 있던 탓이기도 하다. Golang은 기본적으로 문법 자체에서 map, slice(나한테 아직은 slice는 vector다.) 잘 이용하면 좋겠지만, 얼마 배우지도 않고 사용 한거라 매우 어려웠다. 그래도, 문법에서 map을 지원하는 것은 크게 신기했다.
* package가 많다.  
  사실, 문제를 풀면서 크게 이용할 일은 없다. STL이 없어서 너무 불편했던 나는 package를 찾다가 많은 사람이 Github에 올려놓은 것들을 볼 수 있었고, 사용이 편하다. get을 통해 불러오고 그냥 import 하면 된다.

PS를 통해서 익숙해진 Golang으로 간단하게 개발을 해보려고 한다. 아마 웹 크롤러를 만들 것 같다.


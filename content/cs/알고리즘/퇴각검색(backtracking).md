---
id: 퇴각검색(backtracking)
aliases: []
tags: []
date: "2024-05-08"
description: ""
draft: true
title: 퇴각검색(backtracking)
---

#algorithm #search-algorithm #backtracking 
## 정의

*한정 조건*을 가진 문제를 풀려는 전략이다. 
어떤 문제를 푸는데 있어 모든 경우의 수를 시도하여 문제의 정답을 찾아나간다. 
하지만 *한정 조건* 에서의 모든 경우의 수를 시도하는 것이기 때문에 실제로 상당한 경우의 수들이 배제되기 때문에 단순 다중 for문 보다는 빠르게 해결되는 경우가 많다.

>[!quote]
>모든 경우의 수를 전부 고려하는 알고리즘.
>상태 공간을 트리로 나타낼 수 있을 때 적합한 방식이다. 일종의 트리 탐색 알고리즘이라고도 봐도 된다.
>[나무위키](https://namu.wiki/w/백트래킹)



## 원리

### 예시

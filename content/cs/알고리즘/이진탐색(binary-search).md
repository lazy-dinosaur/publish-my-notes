---
id: 이진탐색(binary-search)
aliases:
  - 이진탐색
  - binary-search
tags:
  - binary-search
  - search-algorithm
  - 이진탐색
date: "2024-05-08"
description: ""
draft: false
title: 이진탐색(binary-search)
---

## 정의

>[!quote] 
>
>**이진 탐색 알고리즘** (binary search algorithm) 은 오름차순으로 정렬된 리스트에서 특정한 값의 위치를 찾는 알고리즘이다. 처음 중간의 값을 임의의 값으로 선택하여, 찾고자 하는 값의 크고 작음을 비교하는 방식을 채택하고 있다. 처음 선택한 중앙값이 만약 찾는 값보다 크면 그 값은 새로운 최댓값이 되며, 작으면 그 값은 새로운 최솟값이 된다. 검색 원리상 정렬된  리스트에만 사용할 수 있다는 단점이 있지만, 검색이 반복될 때마다 목표값을 찾을 확률은 두 배가 되무로 속다가 빠르다는 장점이 있다.
>
>[위키백과](https://ko.wikipedia.org/wiki/이진_검색_알고리즘)

[[탐색 알고리즘(search-algorithm)]] 중 정렬된 배열을 탐색할 때 가장 적합.

> 정렬된 데이터에서 특정한 값을 찾아내는 알고리즘

- 탐색 범위를 반으로 나누어 찾는 값을 포함하는 범위를 좁혀가는 방식으로 동작한다.
- 주로 배열의 인덱스르르 기준으로 배열 내의 값을 탐색하는데 사용되지만, 리스트, 트리 등에서도 사용할 수 있다.
- ==반드시 원소들이 일정한 순서로 정렬된 구조에서만 사용할 수 있다.==
- 시간 복잡도는 O(log n)이다. 대용량 데이터에서 특정값의 위치를 찾는데 용이하다.

## 원리
![이진탐색](https://velog.velcdn.com/images/kwontae1313/post/4b6514c9-54b1-425f-afa1-2f167970f5f0/image.png)
1. 정렬된 배열에서 중간 인덱스(`mid`)를 찾는다.
2. 찾으려는 값(`target`)과 중간 값(`mid_val`)을 비교한다.
3. `target` 이 `mid_val` 보다 작으면 `mid` 를 기준으로 왼쪽 부분 배열을 탐색한다.
   `target` 이 `mid_val` 보다 크면 `mid` 를 기준으로 오른쪽 부분 배열을 탐색한다.
4. 탐색 범위를 반으로 줄인다.
5. 탐색 범위가 더 이상 없을 때까지 위 과정을 반복한다.

### 예시

```python
def binary_search(arr,target):
	left=0
	right=len(arr)-1
	while left<=right:
		mid=(left+right)//2
		if arr[mid]<=target:
			left=mid+1
		else:
			right=mid-1
```


>[! tip]
> - 파이썬의 경우 `bisect` 모듈의 `bisect_left` 혹은 `bisect_right` 함수를 통해 쉽게 구현할 수 있다.
>- 만약 탐색 시간을 줄여야 하는 상황에서 메모리를 사용할 수 있는 상황이 아니라면 이진 탐색을 활용할 수 있는지 고민해 보아야 한다. 
> 
>- [[이진 탐색 트리]] 를 활용하여 배열 뿐만이 아닌 트리구조에서도 활용할 수 있다. 







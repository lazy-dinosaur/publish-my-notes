---
id: H-Index
aliases: []
tags:
  - programmers
  - coding-test
  - binary-search
  - 이진탐색
date: "2024-05-08"
description: ""
draft: false
title: H-Index
---
## 문제 설명
H-Index 는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-index 를 나타내는 값인 h를 구하려고 합니다. 위키백과에 따르면, H-Index는 다음과 같이 구합니다.

어떤 과학자가 발표한 논문 `n` 편 중, `h` 번 이상 인용된 논문이 `h` 편 이상이고 나머지 논문이 `h`번 이하 인용되었다면 `h` 의 최댓값이 이 과학자의 H-Index 입니다.

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index 를 return 하도록 solution 함수를 작성해주세요.

#### 제한사항

- 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
- 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.
- 
#### 입출력 예
| citations   | return |
| ----------- | ------ |
| [3,0,6,1,5] | 3      |
#### 입출력 예 설명

이 과학자가 발표한 논문의 수는 5편이고, 그중 3편의 논문은 3회 이상 인용되었습니다. 그리고 나머지 2편의 논문은 3회 이하 인용되었기 때문에 이 과학자의 H-Index 는3입니다.

## 풀이

- 특정 리스트 내부에서의 위치를 찾는 것이기 때문에 `citations` 리스트를 정렬한 뒤에 [[이진탐색(binary-search)]] 을 활용한다면 쉽게 풀 수 있을것으로 생각되었다.
- 또한 제약 을 보더라도 논문의 수 == $10^3$ , 인용 횟수의 경우 $10^4$ 이기 때문에 최댓값을 찾기위해 하나 하나 루프를 통해 진행하는것은 무리라고 생각 된다.

```python
from bisect import bisect_left

def solution(citations):
	n=len(citations)
	citations.sort()
	
	start=max(citations) # 최댓값을 찾아야 하기때문에 큰 수부터 찾는것이 더 빠르게 찾을 수 있고 중간에 루프를 끝내 불필요한 계산을 스킵할 수 있다.

	while start>0:
		lesser=bisect_left(citations,start)
		
		more=n-lesser
		
		if more >=start and start>=lesser:
			return start
		start-=1

```

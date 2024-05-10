---
id: Rotate Image
aliases: []
tags: []
date: "2024-05-08"
description: ""
draft: false
title: Rotate Image
---

#leetcode #coding-test 

## 문제 원문

>[!info] 문제 링크
>https://leetcode.com/problems/rotate-image/

You are given an `n x n` 2D `matrix` representing an image, rotate the image by **90** degrees (clockwise).

You have to rotate the image [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm), which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/08/28/mat1.jpg)

**Input:** matrix = `[[1,2,3],[4,5,6],[7,8,9]]`
**Output:** `[[7,4,1],[8,5,2],[9,6,3]]`

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/08/28/mat2.jpg)

**Input:** matrix =` [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]`
**Output:** `[[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]`

**Constraints:**

- `n == matrix.length == matrix[i].length`
- `1 <= n <= 20`
- `-1000 <= matrix[i][j] <= 1000`

## 문제 설명

>[!abstract]
>2차원 배열을 시계 방향으로 회전시켜라

>[!Caution] 제한 사항
>n 길이의 정사각형
>n 은 20 을 넘지 않는다.

## 풀이

### 첫번째 접근

n 의 크기가 작기 때문에 이중 루프를 돌려도 무리 없이 통과 가능하다고 생각했다.

이후 회전하기 전과 회전한 이후의 인덱스를 비교하여 규칙을 찾아구현하였다.

x 죄표와 y 좌표를 뒤집어주면서 X 리스트를 반전시켜준다면  비교적 쉽게 구할 수 있다.

```python
class Solution:
	def rotate(self, matrix: List[List[int]]) -> None:
		n=len(matrix)
		new_matrix=[[j for j in range(n)] for i in range(n)] # matrix와 똑같은 크기의 2차배열을 만들어준다.
		for i in range(n):
			for j in range(n):
			# 규칙에 맞게 new_matrix 를 만들어준다
				new_matrix[j][n-1-i]=matrix[i][j]
				
		matrix[:]=new_matrix # 원본 matrix 배열에 복사한다.
		
```

### 리스트 컴프리헨션 활용

리스트 컴프리헨션을 활용하여 한줄 코드로 만들수도 있다.

```python
matrix[:] = [[matrix[j-1][i] for j in range(len(matrix),0,-1)] for i in range(len(matrix))]

```

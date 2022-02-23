```
title: Simple Numpy
date: '2022-02-24'
tags: ['BigData']
draft: false
summary: Befor learning BigData(Simple about Numpy)
```

# Befor learning BigData(Simple about Numpy)

빅데이터 공부를 들어가기 전 Numpy에 대한 간단한 공부

- numpy 사용법 예시

```jsx
import numpy as np
from scipy.sparse import csr_matrix

|1 0 2|
|0 0 3|
|4 5 6|
row = np.array([0,0,1,2,2,2])
col = np.array([0,2,2,0,1,2])
data = np.array([1,2,3,4,5,6])

mat = csr_matrix((data, (raw, col)), shape =(3,3))
print(mat)
(0,0)	1
(0,2)	2
(1,2)	3
(2,0)	4
(2,1)	5
(2,2)	6
print('shape: ', mat.shpae)
shape: (3,3)
print(mat[0])
(0,0)	1
(0,2)	2
print(mat[0].nonzero())
(array([0,0]), array([0,2]))

print(mat[0].nonzero()[0])
[0 0]
print(mat[0].nonzero()[1])
[0 2]
```

```jsx
|3 0|
|1 2|
```

인 numpy array가 있다면 0이 아닌 element들의 행렬 index는 (0,0), (1,0), (1,1)

numpy.nonzero 함수는 index들에서 행은 행대로, 열은 열대로 묶어서 두개의 vector 형태로

(0,1,1)과 (0,0,1)을 리턴

rows, cols = numpy_array.nonzero()

- 행 리스트와 열 리스트 벡터를 rows와 cols 변수에 각각 저장

zip() 함수는 동일한 개수로 이루어진 자료 형을 묶어주는 역할

- zip(rows, cols)라고 하면 (0,0), (1,0), (1,1)의 리스트 생성

## Numpy라이브러리

```jsx
// Element-wise operations
a+b, a-b, a*b, a/b

// Transpose
a.transpose() or a.T

// Inverse matrix
np.linalg.inv(a)

// Matrix multiplication
a@b
```

### reshape

기존 데이터는 유지하고 차원과 형상을 바꿔 줌

- 파라미터로 입력한 차원에 맞게 변경(-1로 설정하면 나머지를 자동으로 맞춤
    - eg) (100,) → (2, 50)
    - eg) (100,) → (2, -1): 1차원은 2로 지정하고 2차원은 자동으로 50이 됨
- 바꾸는 개수가 나눠지지 않는다면 ‘**ValueError.cannot reshpae array of size**’ 에러가 발생
    - eg) (100,) → (3, -1): 100을 3으로 나누면 1이 남아 에러 발생

### broadcasting

Broadcasting은 연산에 사용되는 행렬의 모양이 자동으로 바뀐 뒤 연산되는 것

```jsx
x = np.array([1,2,3])
y = np.array([4,5,6,7])
x = x.reshpae(3,1)
// x = [[1],[2],[3]]
y = y.reshape(1,4)
// y = [[4,5,6,7]]
z = x + y
// z is 3x4 dimensional
// z = [[5 6 7 8]
				[6 7 8 9]
				[7 8 9 10]]
```

![Untitled](Befor%20lear%20bcc4d/Untitled.png)

```jsx
x = np.array([0.1,2,3,4,5])
y = np.array([0,1,2,3,4,5,6,7])
x = x.reshpae(2,3,1)
// x = [[[0]
				 [1]
				 [2]]
			  [[3]
				 [4]
				 [5]]]
y = y.reshape(2,1,4)
// y = [[[0 1 2 3]]
				[[4 5 6 7]]]
z = x + y
// z = [[[0 1 2 3]
				 [1 2 3 4]
				 [2 3 4 5]]
				[[7 8 9 10]
				 [8 9 10 11]
				 [9 10 11 12]]]
```

![Untitled](Befor%20lear%20bcc4d/Untitled%201.png)

![Untitled](Befor%20lear%20bcc4d/Untitled%202.png)
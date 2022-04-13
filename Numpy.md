# Numpy(Numerical Python)      
✔️ 파이썬에서 대규모 다차원 배열을 다룰 수 있게 도와주는 라이브러리   
❓ 리스트에 비해서 빠른 연산을 지원하고 메모리를 효율적으로 사용   
```py
import numpy as np
```

## 배열 만들기
```py
np.array([1, 2, 3, 4, 5])             # array([1 2 3 4 5])
np.array([3, 1.4, 2, 3, 4])           # array([3. 1.4 2. 3. 4.])
np.array([1, 2], [3, 4])              # array([[1 2] [3 4]])
np.array([1, 2, 3, 4], dtype='float') # array([1. 2. 3. 4.])
np.zeros(10, dtype=int)               # array([0 0 0 0 0 0 0 0 0 0])
np.ones((3, 5), dtype=float)          # array([[1. 1. 1. 1. 1.] [1. 1. 1. 1. 1.] [1. 1. 1. 1. 1.]])
np.arange(0, 20, 2)                   # array([ 0  2  4  6  8 10 12 14 16 18])
np.linspace(0, 1, 5)                  # array([0.   0.25 0.5  0.75 1.  ])
np.random.random((2, 2))              # array([[0.91356235 0.58211244] [0.86459221 0.55507578]])
np.random.normal((0, 1, (2, 2))       # 평균, 편차, 행렬
np.random.randint(0, 10, (2, 2))      # 0이상 10미만
```

### dtype
1. `int` - i, int_, int32, int64, i8
2. `float` - f, float_, float32, float64, f8
3. `str` - str, U, U32
4. `bool` - ?, bool_

```py
arr =np.array([1, 2, 3, 4], dtype='float')
print(arr.dtype)       # float64
print(arr.astype(int)) # [1 2 3 4]
```

## 배열의 기초
```py
x = np.random.randint(10, size=(3, 4))  # [[3 4 5 6] [6 3 3 6] [7 2 9 9]]
print(x.ndim)  # 차원: 2
print(x.shape) # 모양: (3, 4)
print(x.size)  # 갯수: 12
print(x.dtype) # 타입: int64
```

## Reshape, 이어 붙이고 나누기
### 이어 붙이기
```py
x = np.arange(8)
x2 = x.reshape(2, 4)
print(x2) # [[0 1 2 3] [4 5 6 7]]
```
```py
x = np.array([0, 1, 2])
y = np.array([3, 4, 5])
print(np.concatenate([x, y])) # [0 1 2 3 4 5]
```
```py
matrix = np.arange(4).reshape(2, 2)
print(np.concatenate([matrix, matrix], axis=0)) # [[0 1] [2 3] [0 1] [2 3]]
print(np.concatenate([matrix, matrix], axis=1)) # [[0 1 0 1] [2 3 2 3]]
```
### 나누기
```py
matrix = np.arange(16).reshape(4, 4)
upper, lower = np.split(matrix, [3], axis=0)
print(upper)  # [[ 0  1  2  3] [ 4  5  6  7] [ 8  9 10 11]]
print(lower)  # [[12 13 14 15]]
```
```py
matrix = np.arange(16).reshape(4, 4)
upper, lower = np.split(matrix, [3], axis=1)
print(upper)  # [[ 0  1  2] [ 4  5  6] [ 8  9 10] [12 13 14]]
print(lower)  # [[ 3] [ 7] [11] [15]]
```

## Numpy 연산   
❓ 루프 연산은 느림   
```py
x = np.arange(4)
print(x + 5)  # [5 6 7 8]
print(x - 5)  # [-5 -4 -3 -2]
print(x * 5)  # [ 0  5 10 15]
print(x / 5)  # [0.  0.2 0.4 0.6]
```
```py
x = np.arange(4).reshape((2, 2))
y = np.random.randint(10, size=(2, 2))
print(x)      # [[0 1] [2 3]]
print(y)      # [[1 4] [8 2]]
print(x + y)  # [[ 1  5] [10  5]]
print(x - y)  # [[-1 -3] [-6  1]] 
```

## 브로드캐스팅   
✔️ shape이 다른 array끼리 연산, 부족한 차원에서 차원을 추가해서 계산   
```py
x = np.arange(3).reshape((3, 1))
y = np.arange(3)

print(x + y)  # [[0 1 2] [1 2 3] [2 3 4]]
```

## 집계함수와 마스킹연산   
✔️ 데이터에 대한 요약 통계를 볼 수 있음   
```py
x = np.arange(8).reshape((2, 4))
print(np.sum(x))  # 28
print(np.sum(x, axis=0) # [4 6 8 19]
print(np.sum(x, axis=1) # [6 22]
print(np.min(x))  # 0
print(np.max(x))  # 7
print(np.mean(x)) # 3.5 평균
print(np.std(x))  # 2.29128784747792 표준편차
```   
✔️ True, False array를 통해서 특정 값들을 뽑아내는 방법   
```py
x = np.arange(5)
print(x < 3)    # [ True  True  True False False]
print(x > 5)    # [False False False False False]
print(x[x < 3]) # [0 1 2]
```
---


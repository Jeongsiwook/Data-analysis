# 파일 다루기
## 파일 열기/닫기   
✔️ 파일을 열었다면 꼭 닫아줘야 함   
```py
file = open('data.txt')
content = file.read()
file.close()
```   
✔️ 파일을 자동으로 닫아줌   
```py
with open('data.txt') as file:
  content = file.read()
```  

## 줄 단위로 읽기
```py
contents = []
with open('data.txt') as file:
  for line in file:
    content.append(line)
```

## 파일의 모드   
✔️ 기본은 읽기 모드   
```py
# 쓰기 모드
with open('data.txt', 'w') as file:
  file.write('Hello')
```

---

# 데이터 구조 다루기
## 튜플   
✔️ 순서가 있는 원소들의 집합   
- 각 원소의 값을 수정할 수 없음 
- 원소의 갯수를 바꿀 수 없음

## 리스트로 리스트 만들기    
✔️ list comprehension   
```py
numbers = [1, 3, 4, 5, 6, 7]
even = [n for n in numbers if n % 2 == 0]
```

## 데이터 정렬하기
```py
fruits = ['cherry', 'apple', 'banana']
sort_by_last = sorted(fruits, key=reverse)
```

## 그래프 다루기   
✔️ matplotlib(Mathematical Plot Library)   
- 파이썬에서 그래프를 그릴 수 있게 하는 라이브러리   
- 꺾은선 그래프, 막대 그래프 등을 모두 지원

```py
import matplotlib.pyplot as plt

years = [2013, 2014, 2015, 2016, 2017]
temperatures = [5, 10, 15, 20, 17]

def draw_graph():
  # 막대 그래프의 막대 위치를 결정하는 pos 선언
  pos = range(len(years))
  
  # 높이가 온도인 막대 그래프를 그림
  # 각 막대를 가운데 정렬
  plt.bar(pos, temperature, align="center")
  
  # 각 막대에 해당되는 연도를 표기 (실제위치, 나타낼값)
  plt.xticks(pos, years)
  
  # 그래프 출력
  plt.show()

draw_graph()
```

---

# 모듈과 패키지
## 외부 라이브러리 사용하기
```bash
$ pip install 패키지이름
```

## 가상환경   
✔️ 사용된 라이브러리들의 버전이 다른 경우를 막기 위해, 프로젝트 별 가상환경을 구축   
- Pycharm
- venv
- Anaconda
- Colab

---

# ML 파이프라인
![image](https://user-images.githubusercontent.com/48720589/161081906-38f4d422-b29c-4024-8cea-9cf3f88ce52e.png)   

## Iterator, generator   
❓ 한정된 자원으로 인해 대규모 데이터를 많은 연산이 필요한 머신러닝 모델에 한 번에 넣기 불가능   
❓ 저장된 데이터를 조금씩 불러와 모델에게 넣어주고 모델은 데이터의 일부를 보면서 전체 데이터를 학습   

### generator   
✔️ 조금씩 데이터를 불러오는 것   
- `next()`를 사용해서 yield 만날 때까지만 실행
- `yield`는 값을 반환
```py
def finite_generator():
  count = 0
  for i in range(10):
    count += 1
    yield count
    
gen = finite_generator()
next(gen) # 1
next(gen) # 2
next(gen) # 3
```
## Dataloader   
✔️ 데이터를 조금씩 불러와주는 역할   

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
  

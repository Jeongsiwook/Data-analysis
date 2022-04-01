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

### 그래프 설정
```py
font = fm.FontProperties(fname='./NanumBarungothic.ttf')          # 폰트 설정
plt.xticks(pos, dates, rotation='vertical', fontproperties=font)  # 각 막대에 해당되는 단어 입력
plt.title('1월 중 기온 변화', fontproperties=font)
plt.ylabel('온도', fontproperties=font)                          
plt.tight_layout()                                                # 여백 조정
```
---

# 모듈과 패키지
## 모듈과 패키지   
✔️ 모듈 -> 패키지 -> 라이브러리   
- 모듈: 함수나 변수 또는 클래스를 모아 놓은 파일
- 패키지: 연관된 여러 모듈의 묶음
- 라이브러리: 여러 모듈과 패키지를 묶어 부르는 말   

## 모듈 불러오기   
✔️ import 키워드를 이용해 다른 모듈의 함수, 변수, 클래스를 불러올 수 있음   
✔️ from 키워드를 통해 특정 함수, 변수, 클래스를 불러올 수 있음  
1. 같은 파일 내에서 실행했을 경우
```py
# my_module.py
def plus(a, b):
  c = a + b
  return c

# main.py
import my_module
print(my_module.plus(2, 3))

import my_module as mm
print(mm.plus(2, 3))

from my_module import plus
print(plus(2, 3))

from my_module import *
print(plus(2, 3))
```

2. 다른 파일에서 실행했을 경우
- `import 상위패키지.하위패키지.모듈` -> `상위패키지.하위패키지.모듈.함수()`
- `from 상위패키지.하위패키지 import 모듈` -> `모듈.함수()`
- `from 상위패키지.하위패키지.모듈 import 함수` -> `함수()`

### __init__.py   
✔️ 이 폴더가 패키지라고 말해줌
- __init__.py 파일에서 import
- 패키지를 호출하면 자동으로 __init__.py 파일이 샐행
- `from . import 모듈이름`

```py
# apple에 있는 __init__.py
from . import ipad
from . import iphone

# apple 안에 ipad에 있는 __init__.py
from . import draw

# main.py
import Package

apple.ipad.함수()
```
### __name__   
✔️ 직접 만든 모듈을 불러올 때, 원하지 않는 명령이 실행될 수 있음   
- `if __name__ == "__main__"
```py
# my_module.py
def plus(a, b):
  c = a + b
  print(c)
  return c
  
if __name__ == "__main__":
  plus(3, 5)

# main.py
import my_module

my_module.plus(2, 3)  # 5
print(__name__)           # __main__
print(my_module.__name__) # 'my_module.py'
```

### 패키지에서 * import 하기   
✔️ 패키지의 __init__.py코드가 `__all__`이라는 이름의 목록을 제공(1)   
```py
# main.py
from apple import *

iphone.call.sayhello()
ipad.draw.draw_line()

# apple/__init__.py
__all__ = ['iphone', 'ipad']

# apple/iphone/__init__.py
from apple.iphone import call

# apple/ipad/__init__.py
from apple.ipad import draw
```
```py
# main.py
from apple.iphone import *

call.sayhello()

# apple/iphone/__init__.py
__all__ = ['call']
```
   
✔️ 패키지의 __init__.py코드가 `__all__`이라는 이름의 목록을 제공(1)   
```py
# main.py
import apple

apple.iphone.call.sayhello()
apple.call.sayhello()

# apple/__init__.py
from apple.iphone import *
from apple.ipad import *

# apple/iphone/__init__.py
__all__ = ['call']
```
```py
# main.py
from apple import *

iphone.call.sayhello()
call.sayhello()

# 나머진 위와 같음
```

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



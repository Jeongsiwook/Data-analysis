# 자료형 및 기초 문법
## 자료형이 가지고 있는 유용한 함수들 - 문자열
```py
s = "hello"

print(s.capitalize())           # 앞 글자만 대문자로
print(s.upper())                # 전체 문자열을 대문자로
print(s.lower())		# 전체 문자열을 소문자로
print(s.replace('l', '(ell)'))	# 특정 문자열을 다른 문자열로 대체
print('  world '.strip())       # 앞 뒤 공백 제거
print(s.split('l'))             # 특정 문자열 기준으로 나눈 뒤 list로 저장
print(s.startswith('h'))	# 특정 문자열로 시작하는지 boolean 값 반환
print(s)                        # "hello"
```

## iterable 자료형   
✔️ 한 번에 하나의 member를 반환할 수 있음   
- 문자열, 리스트, 딕셔너리, 집합

## destructuring
```py
A = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
for x, y, z in A:
  print(x, y, z)
```

## 딕셔너리 반복문
```py
A = {'a': 123, 'b': 456, 'c': 789}
for x in A:
	print(x)          # 키 값들만 출력
  
for x in A.items():
	print(x)          # (키, 값) 출력

for key, value in A.items():
	print(key, value)
```

## 반복문과 관련된 유용한 함수들
```py
for idx, value in enumerate(['a', 'b', 'c']):
  print(idx, value)
  
  
numbers = [1, 2, 3]
letters = ['a', 'b', 'c']
for pair in zip(numbers, letters):
  print(pair) # (numbers[i], letters[i]) 출력
```

---

# 함수
## 함수   
❓ 단순화 - 내부 동작 방법을 몰라도 기능을 사용할 수 있음   
❓ 구조화 - 프로그램을 단위별로 작성 가능   
❓ 중복 제거   

1. 내장함수 - `print()`, `range()`, ...
2. 사용자 정의함수
3. 메서드 - `string.upper()`, ...

## 함수와 관련된 유용한 문법: lambda, map
```py
def getSum(a, b, c):
  res = a + b + c
  return res

def getValue(value):
  print(value)
  
# lambda
getSum = lambda a, b, c: a + b + c

# map(함수, iterable)
list(map(getName, ['a', 'b', 'c'])) # 순서대로 출력
```

## 함수와 관련된 지식: call by reference, call by value   
✔️ Python은 mutable, immutable에 따라 매개변수의 call by reference, call by value 결정   
- mutable: 숫자형, 문자열, 튜플, 불리언
- immutable: 리스트, 집합, 딕셔너리
```py
def cal1(data):
  data = data + 1
  
def cal2(data):
  data[0] = data[0] + 1

data1 = 1
data2 = [1]
cal1(data1) # 1 출력
cal2(data2) # [2] 출력
```

---

# 클래스
## 기본 문법
```py
class Cal:
  a = 0               # 클래스 변수: 인스턴스 간에 공유하는 변수
  def __init__(self): # 인스턴스를 부를 때 자동으로 호출되는 특별한 함수
    self.result = 0   # 멤버 변수
    Cal.a += 3
  def add(self, num): # 메서드
    self.result += num
    result self.result
    
cal1 = Cal()  # 인스턴스 생성
cal2 = Cal()
print(cal1.add(3))              # 3
print(cal2.add(7))              # 7
print(cal1.result, cal2.result) # 3 7
```

### __dict__ 메서드   
✔️ 인스턴스의 속성 정보를 dictionary로 반환   
```py
class Car():
  car_count = 10
  def __init__(self, company):
    self.company = company

car1 = Car('Hyundai')
print(car1.__dict__)  # {'company': 'Hyundai'}
```

## 클래스의 상속   
✔️ 상속받을 class 명을 괄호에 넣어줌   
```py
class Cal2(Cal): 
  pass
```

## 클래스의 상속 및 오버라이딩   
✔️ 기존 클래스 속성에 접근 하기 위해선 `super()`를 사용    
```py
class Person:
	def __init__(self, fname, lname):
		self.first = fname
		self.last = lname
	def printname(self):
		print(self.first, self.last)

x = Person("John", "Doe")
x.printname()

class Student(Person):
	def printname(self):
		super().printname() 
		print("S", self.first, self.last)

x = Student("Mike", "Olsen")
x.printname()
```

---

# 예외 처리
## 예외 처리
```py
try:
  pass    # 일단 실행할 코드
except:
  print() # 예외가 발생했을 때 실행할 코드
else:
  print() # 예외가 발생하지 않았을 때 실행할 코드
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

## Tip   
1. format   
✔️ 문자열 중간중간에 특정 변수의 값을 넣어주기 위해 사용   
```py
a = 2
b = 3
print('{} x {} = {}'.format(a, b, a * b))
```
# Pandas   
✔️ 구조화된 데이터를 효과적으로 처리하고 저장할 수 있는 파이썬 라이브러리   
- numpy를 기반으로 만들어져서 다양한 기능들을 제공함
```py
import pandas as pd
```

## Series 데이터   
✔️ numpy array가 보강된 형태 data와 index를 가지고 있음   
```py
data = pd.Series([1, 2, 3, 4])
print(data)
"""
0    1
1    2
2    3
3    4
dtype: int64
"""
```
```py
data = pd.Series([1, 2, 3, 4], index=['a', 'b', 'c', 'd'])
print(data['b'])  # 2
```

### 딕셔너리
```py
population_dict = {
	'korea': 5180,
	'japan': 12718,
	'china': 141500,
	'usa': 32676
}

print(pd.Series(population_dict))
"""
korea      5180
japan     12718
china    141500
usa       32676
dtype: int64
"""
```

## DataFrame   
✔️ 여러 개의 Series가 모여서 행과 열을 이룬 데이터   
```py
gdp_dict = {
	'korea': 5180,
	'japan': 12718,
	'china': 141500,
	'usa': 32676
}
gdp = pd.Series(gdp_dict)
country = pd.DataFrame({
	'population': population,
	'gdp': gdp
})

print(country.index)    # ['china' 'japan' 'korea' 'usa']
print(country.columns)  # ['gdp' 'population']
```

### 연산   
✔️ numpy array처럼 연산자를 쓸 수 있음   

## 저장과 불러오기   
```py
country.to_csv("./country.csv")
country.to_excel("country.xlsx")

country = pd.read_csv("./country.csv")
country = pd.read_excel("country.xlsx")
```

## indexing / slicing   
✔️ `loc` 명시적인 인덱스를 참조하는 인덱싱/슬라이싱   
```py
country.loc['china']
country.loc['japan':'korea', :'population']
```   
✔️ `iloc` 파이썬 스타일 정수 인덱스 인덱싱/슬라이싱   
```py
country.iloc[0]
country.ilock[1:3, :2]
```   

## DataFrame 새 데이터 추가/수정   
- 리스트로 추가하는 방법과 딕셔너리로 추가하는 방법
```py
dataframe = pd.DataFrame(columns=['이름', '나이', '주소'])
dataframe.loc[0] = ['임원균', '26', '서울']
dataframe.loc[1] = {'이름': '철수', '나이': '25', '주소': '인천'}
dataframe.loc[1, '이름'] = '영희'
print(dataframe)
"""
    이름  나이  주소
0  임원균  26  서울
1   영희  25  인천
"""
```
- 새로운 컬럼 추가
```py
dataframe['전화번호'] = np.nan
dataframe.loc[0, '전화번호'] = '01012341234'
```
- 컬럼 선택하기
```py
print(dataframe['이름'])
print(dataframe[['이름', '주소', '나이']])
```

## 연산과 함수
- 사칙 연산 모두 가능
```py
dataframe.isnull()  # nan 또는 None일 때 True
dataframe.notnull() # 반대
dataframe.dropna()  # 누락된 데이터를 삭제
dataframe['전화번호'] = dataframe['전화번호'].fillna('전화번호 없음') # 누락된 데이터 채우기
```
```py
a = pd.Series([2, 4, 6], index=[0, 1, 2])
b = pd.Series([1, 3, 5], index=[1, 2, 3])
print(a + b)
print(a.add(b, fill_value=0))
"""
0    NaN
1    5.0
2    9.0
3    NaN
dtype: float64
0    2.0
1    5.0
2    9.0
3    5.0
dtype: float64
"""
```
```py
data = {
	'A': [i + 5 for i in range(3)],
	'B': [i ** 2 for i in range(3)]
}
df = pd.DataFrame(data)
print(df['A'].sum())
print(df.sum())
print(df.mean())
"""
18
A    18
B     5
dtype: int64
A    6.000000
B    1.666667
dtype: float64
"""
```

## 값으로 정렬하기
```py
df.sort_values('col1')                  # 오름차순
df.sort_values('col1', ascending=False) # 내림차순
df.sort_values(['col2', 'col1'])        # col2를 우선으로 정렬 후, 같으면 col1으로 정렬
df.sort_values(['col2', 'col1'], ascending=[True, False]) # col2를 기준으로 오름차순으로, col1을 기준으로 내림차순
```

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
---

## 조건으로 검색하기   
✔️ Numpy array와 마찬가지로 masking 연산이 가능   
```py
df = pd.DataFrame(np.random.rand(5, 2), columns=["A", "B"])
print(df["A"] < 0.5
"""
0    False
1    False
2     True
3     True
4    False
Name: A, dtype: bool
"""
```
```py
df = pd.DataFrame(np.random.rand(5, 2), columns=["A", "B"])
print(df[(df["A"] < 0.5) & (df["B"] > 0.3)])
print(df.query("A < 0.5 and B > 0.3"))
"""
          A         B
1  0.309814  0.899958
4  0.269490  0.655596
"""
```
```py
df["Animal"].str.contains("Cat") # 특정 열에서 Cat을 포함하면 True	
df.Animal.str.match("Cat")	 # 특정 열에서 Cat이라면 True
```

## 함수로 데이터 처리하기   
✔️ `apply`   
```py
df = pd.DataFrame(np.arange(5), columns=["Num"])
def square(x):
	return x ** 2
df["square"] = df["Num"].apply(square)
df["square"] = df.Num.apply(lambda x: x ** 2)
print(df)
"""
   Num  square
0    0       0
1    1       1
2    2       4
3    3       9
4    4      16
"""
```   
✔️ `replace` apply 기능에서 데이터 값만 대체     
```py
df["Sex"] = df.Sex.replace({"Male": 0, "Female": 1})
df.Sex.replace({"Male": 0, "Female": 1}, inplace=True)	# 그대로 바꿀 수 있음
```

## 그룹으로 묶기   
✔️ 간단한 집계를 넘어서 조건부로 집계하고 싶은 경우   
```py
df = pd.DataFrame({
	"key": ['A', 'B', 'C', 'A', 'B', 'C'],
	'data1': [1, 2, 3, 1, 2, 3],
	'data2': np.random.randint(0, 6, 6)
})

print(df.groupby('key').sum())
print(df.groupby(['key', 'data1']).sum())
"""
     data1  data2
key              
A        2      9
B        4      4
C        6      5
           data2
key data1       
A   1          9
B   2          4
C   3          5
"""
```   
✔️ `aggregate` groupby를 통해서 집계를 한 번에 계산   
```py
print(df.groupby('key').aggregate(['min', np.median, max]))
print(df.groupby('key').aggregate({'data1': 'min', 'data2': np.sum}))
"""
    data1            data2           
      min median max   min median max
key                                  
A       1    1.0   1     0    0.5   1
B       2    2.0   2     0    0.0   0
C       3    3.0   3     0    0.5   1
     data1  data2
key              
A        1      1
B        2      0
C        3      1
"""
```   
✔️ `filter` groupby를 통해서 그룹 속성을 기준으로 데이터 필터링   
```py
def filter_by_mean(x):
	return x['data2'].mean() > 3
	
print(df.groupby('key').mean())
print(df.groupby('key').filter(filter_by_mean))
"""
     data1  data2
key              
A      1.0    3.0
B      2.0    1.5
C      3.0    3.5
  key  data1  data2
2   C      3      4
5   C      3      3
"""
```   
✔️ `apply` groupby를 통해서 묶인 데이터에 함수 적용   
```py
print(df.groupby('key').apply(lambda x: x.max() - x.min()))
"""
     data1  data2
key              
A        0      2
B        0      1
C        0      4
"""
```   
✔️ `get_group` groupby로 묶인 데이터에서 key값으로 데이터를 가져올 수 있음   
```py
df = pd.read_csv("./univ.csv")
df.head()
print(df.groupby("시도").get_group("충남"))	# 시도로 묶은 후 충남에 있는 걸 가져옴
```

## Multiindex 와 pivot_table   
✔️ 인덱스를 계층적으로 만들 수 있음   
- 인덱스 탐색의 경우에는 loc, iloc 사용 가능
```py
df = pd.DataFrame(
	np.random.rand(4, 2),
	index = [['A', 'A', 'B', 'B'], [1, 2, 1, 2]],
	columns = ['data1', 'data2']
)

print(df)
"""
        data1     data2
A 1  0.316835  0.896373
  2  0.219161  0.758219
B 1  0.169113  0.137406
  2  0.663948  0.221704
"""
```
```py
df = pd.DataFrame(
	np.random.rand(4, 4),
	columns = [['A', 'A', 'B', 'B'], [1, 2, 1, 2]]
)

print(df)
print(df["A"])
print(df["A"]["1"])
"""
          A                   B          
          1         2         1         2
0  0.095091  0.836691  0.116218  0.163103
1  0.387552  0.024354  0.055606  0.763126
2  0.714593  0.581538  0.101401  0.527408
3  0.407615  0.561805  0.033892  0.389331
          1         2
0  0.095091  0.836691
1  0.387552  0.024354
2  0.714593  0.581538
3  0.407615  0.561805
0    0.095091
1    0.387552
2    0.714593
3    0.407615
Name: 1, dtype: float64
"""
```   
✔️ 데이터에서 필요한 자료만 뽑아서 새롭게 요약, 분석 할 수 있는 기능
- 엑셀에서의 피봇 테이블과 같음
- index는 행 인덱스로 들어갈 key
- column에 열 인덱스로 라벨링될 값 value에 분석할 데이터
```py
df.pivot_table(
	index='sex', columns='class', values='survived',
	aggfunc=np.mean
)
```
```py
df.pivot_table(
	index="월별", columns="내역", values=["수입", "지출"]
)
```
---


# Matplotlib   
✔️ 파이썬에서 데이터를 그래프나 차트로 시각화할 수 있는 라이브러리   
```py
import matplotlib.pyplot as plt
```

## 그래프 그려보기
1. state machine interface
```py
x = [1, 2, 3, 4, 5]
y = [1, 2, 3, 4, 5]
plt.plot(x, y)
plt.title("First Plot")
plt.xlabel("x")
plt.ylabel("y")
```
2. object oriented interface
```py
x = [1, 2, 3, 4, 5]
y = [1, 2, 3, 4, 5]
fig, ax = plt.subplots()  # 전체 도화지, 하나의 그래프
ax.plot(x, y)
ax.set_title("First Plot")
ax.set_xlabel("x")
ax.set_ylabel("y")
fig.set_dpi(300)
fig.savefig("first_plot.png")
```

### 여러개 그래프 그리기
```py
x = np.linspace(0, np.pi * 4, 100)  # 0 부터 4pi까지 100개의 구간으로 나눔
fig, axes = plt.subplots(2, 1)      # 행 2, 열 1
axes[0].plot(x, np.sin(x))
axes[1].plot(x, np.cos(x))
```

## 그래프들
1. Line plot
- *Line style*
  - `-` solid
  - `--` dashed
  - `-.` dashdot
  - `:` dotted

- *Color*
  - `r` red
  - `green` green
  - `0.8` 0 ~ 1
  - `#524FA1`

- *Marker*
  - `.` 작은 점
  - `o` 큰 점
  - `v` 화살표
  - `s` 네모
  - `*` 별표
```py
fig, ax = plt.subplots()
x = np.arange(15)
y = x ** 2
ax.plot(
  x, y,
  linestyle=":",
  marker="*",
  color="#524FA1"
)
```
2. 축 경계 조정하기
```py
x = np.linespace(0, 10, 1000)
fig, ax = plt.subplots()
ax.plot(x, np.sin(x))
ax.set_xlim(-2, 12)             # x, 시작과 끝 지정
ax.set_ylim(-1.5, 1.5)          # y, 시작과 끝 지정
```
3. 범례
```py
fig, ax = plt.subplots()
ax.plot(x, x, label='y=x')
ax.plot(x, x**2, label='y=x^2')
ax.set_xlabel("x")
ax.set_ylabel("y")
ax.legend(
  loc='upper right',  # 위치, lower, upper, center
  shadow=True,        # 그림자
  fancybox=True,      # 모서리를 둥글게
  borderpad=2         # padding
)
```

## Scatter
```py
fig, ax = plt.subplots()
x = np.arange(10)
ax.plot(
  x, x**2, "o",             # marker를 넣으면 scatter 그래프
  markersize=15,
  markerfacecolor='white',  # marker 안쪽 색
  markeredgecolor="blue"    # marker 선 색
)
```
```py
ax.scatter(
  x, y, c=색, s=사이즈, alpha=0.3 # 투명도
)
```

## Bar 와 Histogram
```py
x = np.arange(10)
fig, ax = plt.subplots(figsize=(12, 4))
ax.bar(x, x*2)
```
```py
x = np.random.rand(3)
y = np.random.rand(3)
z = np.random.rand(3)
data = [x, y, z]

fig, ax = plt.subplots()
x_ax = np.arange(3)
for i in x_ax:
  ax.bar(x_ax, data[i], bottom=np.sum(data[:i], axis=0))
ax.set_xticks(x_ax)
ax.set_xticklabels(["A", "B", "C"])
```
```py
fig, ax = plt.subplots()
data = np.random.randn(1000)  # 표준정규분포에서 1000개 데이터
ax.hist(data, bins=50)        # bins 막대기를 몇개로 나눌 것인지,클수록 막대 얇음
```

### 한글을 지원하는 폰트 사용
```py
import matplotlib.font_manager as fm
fname='./NanumBarunGothic.ttf'
font = fm.FontProperties(fname = fname).get_name()
plt.rcParams["font.family"] = font
```

## Matplotlib with Pandas
```py
df = pd.read_csv("./president_heights.csv")
fig, ax = plt.subplots()
ax.plot(df["order"], df["height(cm)"], label="height")
ax.set_xlabel("order")
ax.set_ylabel("height(cm)")
```
---

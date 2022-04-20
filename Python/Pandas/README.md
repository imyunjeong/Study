Reference : https://rfriend.tistory.com/263

1. [인데스 접근](#1-인덱스-접근)
2. [결측값 처리](#2-결측값-처리)


## 1. 인덱스(index) 접근: `.loc()`, `.iloc()`, `.ix()`, `.at()`

- `.loc()` : label-based indexing 사용O, integer position 사용X
- `.iloc()`: integer position 사용O, label 사용X
- `.ix()`  : label과 integer position 모두 사용O

```python
>>> s = pd.Series(np.nan, index=[49, 48, 47, 46, 1, 2, 3, 4])
>>> s
49   NaN
48   NaN
47   NaN
46   NaN
1    NaN
2    NaN
3    NaN
4    NaN

>>> s.loc[:2] # slice up to and including label 2
49   NaN
48   NaN
47   NaN
46   NaN
1    NaN
2    NaN

>>> s.iloc[:2] # slice the first three rows
49   NaN
48   NaN

>>> s.ix[:2] # the integer is in the index so s.ix[:2] works like loc
49   NaN
48   NaN
47   NaN
46   NaN
1    NaN
2    NaN

>>> s.iloc[:6]
49   NaN
48   NaN
47   NaN
46   NaN
45   NaN
1    NaN

>>> s.loc[:6]
KeyError: 6

>>> s.ix[:6]
KeyError: 6
```
- iloc정수 위치에 따라 작동합니다. 따라서 행 레이블이 무엇이든 관계없이 항상 첫 번째 행을 가져올 수 있습니다.
- df.iloc[0]
- df.iloc[-5:]   = df.head(5)  # 마지막 다섯 행을 수행
- df.iloc[:, 2]    # the : in the first position indicates all rows  # 세 번째 열을 검색
- df['time']    # equivalent to df.loc[:, 'time']
- df.loc['b':, 'date']   # equivalent to df.iloc[1:, 1]
- df.loc['a']     # equivalent to df.iloc[0]


## 2. read_csv() 
- read_csv() 사용 시 날짜를 datetime 형태로 불러오기
- csv 의 특정 컬럼 중 날짜형태(yyyy-MM-dd hh:mi:ss) 로 표시되어 있어도 csv를 불러오면 object(string) 형태로 선언되어 있다.
- 이전까지는 padnas.to_datetime 을 이용해서 형태를 바꿨는데 데이터가 1000만 건이상이 되면 변환해주는것도 시간이 꽤 소요된다.
- 그래서 옵션을 추가해 처음 로드할때 부터 데이터타입을 맞추는게 더 효율적이다.
- read_csv를 이용할때 옵션을 주면 datetime 형태로 로드가 가능하다
```python
>>> dt = pd.read_csv('sample2.csv')
>>> dt.dtypes
id     int64
상품명  object
구매일  object     # 아무런 옵션을 주지 않으면 위와 같이 구매일이 object 로 지정되어 있다.
dtype: object

# 1) 이 상태에서 pd.to_datetime 를 이용해 날짜를 바꿀 수 있다.
>>> df['구매일'] = pd.to_datetime(df['구매일'])
>>> df.dtypes
id     int64
상품명  object
구매일  datetime64[ns]
dtype: object

# 2) csv 파일을 로드할 때 parse_dates 옵션을 추가
>>> df = pd.read_csv('sample2.csv', parse_dates=['구매일'])  # datetime 형태로 변경되어야 하는 컬럼명을 지정한다
```


## 2. 결측값(None 또는 np.nan) 처리: `.dropna()`

- 결측값이 들어 있는 행 전체 제거(Delete row with missing values)
  - `df.dropna(axis=0)`
- 결측값이 들어 있는 열 전체 제거(Delete column with missing values) 
  - `df.dropna(axis=1)`
- 특정 행/열만 대상으로 결측값이 있으면 제거
  - `df['A'].dropna()`
  - `df[['A', 'B']].dropna()`


```python
>>> df.ix[[0,1], 'A'] = None
>>> df.ix[2, 'B'] = np.nan

# 메세지 : .ix is deprecated. Please use .loc for label based indexing or .iloc for positional indexing
# 근데 .ix()에 문제가 있어 곧 사라진다고 한다. .loc이나 .iloc 등을 사용하는 것을 권장
# 같은 기능을 하는 .at()을 사용할 때는 메시지가 안뜬다 
>>> df.ix[0]['A'] = 0 # index가 0이고, column이 A인 값을 0으로 수정
```

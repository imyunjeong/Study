## python 내장 함수: `all()` & `any()`

1. [all](#1-all)
2. [any](#2-any)


- all과 any는 **반복가능한 자료형(Iterable)을 인자로 받음**
- Iterable 자료형: List, Tuple, Set, Dictionary, String (=for문에서 사용가능한 것들)


## 1. all
```python
def all(iterable):
    for element in iterable:
        if not element:
            return False
        return True
```
- `all(iterable)`: 인자로 받은 반복 가능한 자료형(iterable)의 **모든 요소가 참(True)이면 참(True)를 반환**하는 함수
- and의 특징을 가진 함수
  - 인자로 반복 가능한 (iterable) 자료형을 받음
  - 인자로 받은 데이터의 모든 요소가 True이어야지 True를 반환
  - 인자로 받은 요소 중 하나라도 False이면 False를 반환
  - 인자로 받은 요소가 비어 있으면 True

```python
>>> all([1,2,3,4,5])    # 리스트 요소에 True만 있는 경우 => True
>>> all([0,1,2,3,4])    # 리스트 요소에 False(0 == False)가 있는 경우: => False
>>> all([])             # 리스트 요소가 빈 경우 => True
>>> all(['a','',2,3])   # 리스트 요소에 빈 문자열이 있는 경우 => False
```


## 2. any
```python
def any(iterable):
    for element in iterable:
        if element:
            return True
    return False
```
- `any(iterable)`: 인자로 받은 반복가능한 자료형(iterable) 중 **단 하나라도 참(True)이 있으면 참(True)를 반환**하는 함수 
- 반대로, **모든 요소가 거짓(False)인 경우에만 거짓(False)을 반환**
- or의 특징을 가진 함수
  - 인자로 받은 요소 중 하나라도 True면 True를 반환
  - False가 몇개든 상관없이 단 하나라도 True면 True 반환
  - 모든 요소가 False인 경우에만 False 반환
  - 인자로 받은 자료형이 비어있는 경우 False 반환


```python
>>> any([1,2,3,4,5])   # True
>>> any([0,1,2,3,4])   # True
>>> any([])            # False
>>> any('')            # False
>>> any(['a','',2,3])  # True
```

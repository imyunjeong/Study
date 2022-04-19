# 파이썬 코드 레시피 302
<img src="http://image.kyobobook.co.kr/images/book/large/728/l9791191600728.jpg" width="15%" height="15%">

* 읽은 기간: 2022-04-19 ~ 

### 목차

## 003. 파이썬 코드 구조의 특징
- 독스트링(Docstring): 함수나 클래스의 설명을 입력. 작은/큰따옴표 3개를 사용한다. 변수에 대입해 문자열로 다룰 수도 있다.
  ```python
  # 큰따옴표 3개를 사용하면 docstring이 된다.
  >>> def main():
          """
          여기에 함수의 설명을 입력
          """
  ```

- `pass()`는 아무것도 하지 않는 구문. 처리를 수행하고 싶지 않을 때 명시적으로 입력한다. 들여쓰기 않에 공백만 존재하면(아무런 내용이 없으면) SyntaxError가 발생한다.


- 코드 줄바꿈: 한 구문의 길이가 길어지면 중간에 `\`를 사용해 줄바꿈(개행)을 할 수 있다. 
  - 단, 함수의 인수, 튜플, 리스트, 딕셔너리 등 (), [], {}로 감싸인 부부은 식별자나 수치, 문자열 중간이 아니라면 \를 붙이지 않아도 줄바꿈을 할 수 있다.
  ```python 
  >>> y = 1+2+3+4+5 \ 
          +6+7+8+9+10
  ```

```python 
# 파이썬 명령어로 실행했을 때만 처리하고 싶을 때 스크립트에 입력한다.
if __name__ == "__main__":
```

## 005. print 함수의 출력 커스터마이즈하기
- `sep()` : 구분 문자 변경
  ```python
  >>> x = 100
  >>> y = 200
  >>> z = 300
  >>> print(x, y, x)            # print 함수로 여러 변수를 나열해 출력하면 기본적으로 공백으로 출력
  100 200 300
  >>> print(x, y, z, sep=',')   # 인수 sep에 임의의 구분 문자를 쉼표(,)로 지정해서 출력
  100,200,300
  ```

- `end()` : 끝 문자 변경
  ```python
  >>> for i in range(0, 2):
  >>>     print(i)              # print 함수로 출력하면 끝 문자는 기본적으로 줄바꿈 문자가 됨
  0
  1
  2
  >>> for i in range(0, 2):
  >>>     print(i, end='')     # 줄바꿈을 하지 않고 출력
  012
  ```
  
  ```python 
  # sep="," 과 end="," 은 서로 다름
  
  >>> for i in range(0, 2):
  >>>     print(i, sep=',')   # 하나의 변수를 나열하기 때문에 구분 문자 쉼표(,)가 작동하지 않음
  0
  1
  2
  >>> for i in range(0, 2):
  >>>     print(i, end=',')
  0,1,2
  
  >>> for k, v in list(enumerate(range(0,2))):
  >>>     print(k, v, sep=',')
  0,0
  1,1
  2,2
  >>> for k, v in list(enumerate(range(0,2))):
  >>>     print(k, v, end=',')
  0 0,1 1,2 2
  ```
  
## 006. 모듈 임포트하기
- 파이썬 스크립트는 모듈(module), 다시 말해 부품이며 다른 스크립트에서 특정 기능을 호출해 이용할 수 있다.
- 모듈을 하나로 모은 것을 패키지(package)라 부르며, 모듈과 패키지를 라이브러리(library)라고 한다.
- 파이썬에서 기본으로 제공하는 패키지나 모듈을 '표준 라이브러리'라고 한다. 한편, 제삼자가 만든 것은 '서드 파티 라이브러리'라고 부르며 `pip` 명령어로 설치해야 한다. 직접 작성한 스크립트에서 모듈이나 패키지를 만들 수도 있다.

- `import 모듈 as 별명` : 모듈을 임포트                                (보통은 import 함수)
- `from 모듈 import 임포트_대상 as 별명` : 모듈의 특정 속성만 임포트     (보통은 from 클래스 import 함수)


```python
# import 문: 모듈이나 패키지는 import 문으로 이용할 수 있다. 임포트한 모듈 내부의 속성에 접근하고 싶을 때는 마침표(.)로 지정한다.
>>> import math
>>> print(math.pi)       # 표준 라이브러리인 math 모듈의 원주율 pi를 이용

# from으로 필요한 부분만 임포트
>>> from math import pi
>>> print(pi)
```

## 007. pip로 외부 라이브러리 설치하기
- 파이썬은 PyPi라는 서드 파티 라이브러리 저장소(https://pypi.org/)를 무료 공개한다.
- PyPi에서 사용할 라이브러리를 발견했다면 pip 명령어로 설치, 갱신, 삭제 등의 패키지 관리를 할 수 있다.

- `pip install 라이브러리명`          : 라이브러리 설치
- `pip uninstall 라이브러리명`        : 라이브러리 삭제
- `pip install -U 라이브러리명`       : 라이브러리 갱신

- `pip freeze > requirements.txt`    : 설치한 라이브러리 정보를 텍스트 파일에 출력 (설치한 라이브러리 목록 표시)
- `pip install -r requirements.txt`  : 텍스트파일에 기록된 라이브러리 일괄 설치
- `pip uninstall -r requirements.txt`: 텍스트파일에 기록된 라이브러리 일괄 삭제

## 008. vevn로 가상환경 만들기
- 가상 환경 구축     : `python -m venv {가상 환경 경로}`
- 가상환경으로 전환
  |함수|처리|예제|
  |----|---|----|
  |윈도우 명령 프롬프트(cmd)| 가상 환경 디렉터리에서 .\Scripts\activate.bat|venv\Scripts\activate.bat|
  |윈도우 파워셸|가상 환경 디렉터리에서 ./Scripts/Activate.psl|venv/Scripts/Activate.psl|
  |유닉스 계열|가상 환경 디렉터리에서 ./bin/activate를 source 명령어로 로딩|source venv/bin/activate|

- 가상 환경 종료
  |함수|처리|예제|
  |----|---|----|
  |윈도우 명령 프롬프트(cmd)|가상 환경 디렉터리에서 .\Scripts\deactivate.bat|venv\Scritps\deactivate.bat|
  |윈도우 파워셸|deactivate|deactivate|
  |유닉스 계열|deactivate|deactivate|
  

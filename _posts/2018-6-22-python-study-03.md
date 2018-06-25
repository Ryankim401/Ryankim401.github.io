---
layout: post
title: python study 03

## Python study Ep02 데이터 타입



### 변수(Variables)

- 프로그램이 실행되면서 필요한 데이터를 임시로 저장하는 공간

- 효율성을 높이기 위해 적절한 크기 / 용도의 변수에 값을 담아서 처리

- 하나의 소프트웨어가 동작하면서, 로직에 따라 수많은 새로운 변수가 생겨나고 변경되며 제거

  ```python
  name = "Hello, Python."
  birth = 1990
  age = 2017 - birth
  prnit(name, age)
  ```

  `=`  우측에 있는 값을 좌측에 대입한다



### 데이터 타입(Data Types)

- 변수는 하나의 데이터를 담아두는 공간. 그릇 개념
- 효율성을 높이기 위해, 그릇도 목적 (크기/용도) 에 따라 다양한 그릇이 필요
  - 물을 담아두는 다양한 용기 : 물컵, 양동이, 물탱크, 소방차 등
- 자원은 유한하다
  - 아껴써야한다. (CPU, 메모리, 디스크 등)



### 숫자(Numeric Type)

- 정수형 : int
- 실수형 : float
- 사칙연산 (+, -, *, /), 몫(//), 나머지(%), 지수 승(**) 연산자
- Python2에서는 int/long/float/double 형이 존재했지만, Python3 에서는 int/float로 통합
- 수의 범위 제한 없음



### 참 / 거짓(Boolean Type)

- 참은 True, 거짓은 False (Java는 true / false)

- 비교 연산자의 결과는 Boolean Type

  - <. <=, >, >=, ==, !=
  - is, is not : 참조 비교

- 논리 연산자

  - or, and, not

  ```python
  >>> a = []
  >>> b = []
  >>> id(a), id(b)
  (2253248684552, 2253248038088)
  >>> a == b
  True
  >>> a is b
  False
  ```



### 다른 타입에서의 Boolean 판단

- 숫자 0은 False, 그 외에는 True

- 빈 문자열은 False, 그 이외에는 True

- 빈 list / tuple / set / dict 는 False, 그 이외에는 True

  ```python
  >>> bool(0), bool(1), bool(2)
  (False, True, True)
  >>> bool(''), bool(' '), bool('a')
  (False, True, True)
  >>> bool([]), bool(()), bool({}), bool(set()), bool([' '])
  (False, False, False, False, True)
  ```

  

### 문자열(String Type)

- 문자열을 홑따옴표 ('') 또는 쌍따옴표("") 로 감싸기

- 홑(상)따옴표 1개로 감싼 문자열 안에 홑(쌍)따옴표를 문자열로서 처리하고자 할 경우

  해당 홑(쌍) 따옴표를 ESCAPE 처리  ( \ )

  > ![1529746205783](C:\Users\YANGUK\AppData\Local\Temp\1529746205783.png)

  여러줄 문자열을 쉽게 정리할 수 있도록 지원. 홑(쌍)따옴표 3개로 감싸주는 문법

  > ![1529746477439](C:\Users\YANGUK\AppData\Local\Temp\1529746477439.png)



### 문자열 형식 지정자

- 문자열 내에 "{}"와 같은 형태로 슬롯을 만들고, format 함수를 통해 슬롯에 필요한 데이터를 넘김

- format 함수에 함수인자로서 슬롯을 지정하는 방법

  - 함수 위치 인자 (Positional Arguments)

    ```python
    >>> '{0}, {1}, {2}'.format('a', 'b', 'c')
    >>> '{}, {}, {}'.format('a', 'b', 'c')
    >>> '{2}, {1}, {0}'.format('a', 'b', 'c')
    >>> '{2}, {1}, {0}'.format(*'abc')     # unpacking argument sequence
    >>> '{0}, {1}, {2}'.foramt('a', 'b')   # arguments' indices can be 										  repeated
    ```

  - 함수 키워드 인자 (Keyword Arguments)

    ```python
    >>> 'Coordinates : {lat}, {lng}'.format(lat='37.24N', lng='-115.81W')
    >>> coord = {'lat': '37.24N', 'lng': '-115.81W'}
    >>> 'Coordinates : {lat}, {lng}'.format(**coord)
    ```

    

### NameError

- 정의되지 않은 변수에 접근 시에 발생

  ```python
  >>> print(a)
  NameError: name 'a' is not defined
  ```

  

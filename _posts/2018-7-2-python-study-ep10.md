---
catagories: Python
title: Python Study 10
---

## Python study Ep10 코루틴 및 제너레이터

### Co-Routine (코루틴)

- Sub Routine : 일반적인 함수
  - 진입점이 하나이며, 부모 / 자식의 종속적인 관계가 성립
  - 매 호출시마다, Routine 내 context가 초기화
- Co Routine : 코루틴
  - 진입점이 여럿이며, 병렬(Concurrensy, not Parallelism) 수행
  - 호출부와 대등한 관계
  - 여러번 호출이 되어도, Routine 내 Context가 유지



#### Generator 문법으로 간편히 코루틴 구현

```python
def sub_routine():
    return 10
def co_routine():
    yield 10
    yield 20
    yield 30
    
>>> sub_routine()

>>> generator1 = co_routine()
>>> generator1
<generator object co_routine at 0x00000294CEC318E0>
>>> next(generator1)   # 이제서야 루틴이 실행 → 첫 yield까지 수행
10
>>> next(generator1)   # 이어서, 다음 yield까지 수행
20
>>> next(generator1)   # 이어서, 다음 yield까지 수행
30
>>> next(generator1)   # 더 이상 생산(yield)할 수 없으므로, StopIteration 예외                          자동 발생
StopIteration
```

#### Generator

generator는 항상 iterator이다.

- 연속된 (Sequences) 값들을 생산해내는 함수

- 함수에 yield 키워드가 쓰여지면, Generator

- yield 한 값들이 순차적으로 생산된다.

- Generator 에서 return문을 만나더라도 종료만 될 뿐, 리턴값이 사용되지 않는다.

- 추가 yield가 없으면, StopIteration 예외 자동 발생

  - for 루프는 StopIteration 예외를 자동으로 처리

  - 직접 StopIteration 예외를 발생시켜도 된다.

    ```python
    def myxrange(start, end):
        while start < end:
            yield start        # 함수 generator 문법
            start += 1
    ```

    

#### 중첩된 Generator는 Pipeline

- 매 Generator 가 완료된 후에, 다음 Generator가 수행되는 것이 아니라,

- 한 Generator에서 값이 생산될 때마다 다음 Generator로 값이 전달

  ```python
  >>> gen1 = (i**2 for i in range(10))   # gen1에서 0이 생산되자마자
  >>> gen2 = (j+10 for j in gen1)        # gen2로 전달 ... (쭈욱~)
  >>> gen3 = (k*10 for k in gen2)        # gen3로 전달 ...
  
  >>> for i in gen3:   # 첫 번째 값을 받아올 때, 그제서야 gen1에서 값 생산 시작
      	print(i, end=' ')
  100 110 140 190 260 350 460 590 740 910 
  ```

- 데이터가 아무리 많아도, 첫 스타트업 시작이 짧다.

- 그렇기에 가급적이면 list/tuple로 변환하지말고 Generator를 그대로 사용

  ```python
  >>> t1 = tuple(i**2 for i in range(10))  # 모든 값을 tuple로 생성
  >>> t2 = tuple(j+10 for j in t1)         # 모든 값을 tuple로 생성
  >>> t3 = tuple(k*10 for k in t2)         # 모든 값을 tuple로 생성
  
  >>> for i in t3   # 이미 생성된 tuple값에 대해서 순회
          print(i, end=' ')
  100 110 140 190 260 350 460 590 740 910 
  ```

#### iterator로 tuple / list 생성하기

Generator is iterator

```python
def to_3():
	yield 1
	yield 2
	yield 3
    
numbers_list = list(to_3())
numbers_tuple = tuple(to_3())
```



#### tuple / list / iterator를 dict으로 변환

```python
# dict는 key / value 쌍으로 구성
mylist = [['a', 1], ['b', 2]]
dict(mylist) # {'a': 1, 'b': 2}

# key가 중복이 되면, 마지막 key / value 가 남는다.
mylist = [['a', 1], ['b', 2], ['a', 3]]
dict(mylist) # {'a': 3, 'b': 2}

# key / value 쌍이 맞지 않을 경우, ValueError 발생
mylist = [['a', 1], ['b', 2], ['a']]
dict(mylist) # ValueError: dictionary update sequence element #2 has length                              1; 2 is required
```

#### Generator로 피보나치 수열 생산하기

**제한된 크기만큼 생산**

```python
def fib(max_count):
    x, y, count = 1, 1, 0
    while True:
        if count >= max_count:
            break
        yield x
        x, y = y, x + y
        count += 1
        
>>>> for x in fib(10):
         print(x, end=' ')
```

**소비하는 만큼만 생산 (좀 더 범용적으로 활용이 가능)**

```python
def fib():
    x, y = 1, 1
    while True:
        yield x
        x, y = y, x + y
        
>>> count = 0
    for x in fib():
	    print(x, end= ' ')
	    count += 1
	    if count >= 10:
	        break
1 1 2 3 5 8 13 21 34 55 

>>> from itertools import islice
>>> islice(fib(), 10)
<itertools.islice at 0x294ced106d8>
>>> tuple(islice(fib(), 10))
(1, 1, 2, 3, 5, 8, 13, 21, 34, 55)
```



#### list / set / dict Comprehension

- 순회가능한 객체를 조작하여, 필터링 / 새로운 리스트 / 사전 / 집합을 만들 수 있는 방법

- tuple comprehension은 없음. 필요하다면 tuple(순회가능한 객체)

  ```python
  # list comprehension
  [ 표현식 for 변수 in 순회가능한객체 ]
  [ 표현식 for 변수 in 순회가능한객체 if 필터링조건 ]
  
  [i**2 for i in range(5)]                # {0, 1, 4, 9, 16}
  [i**2 for i in range(5) if i%2 == 0]    # {0, 4, 16}
  
  # dict comprehension
  { key:표현식 for 변수 in 순회가능한객체 }
  { key:표현식 for 변수 in 순회가능한객체 if 필터링조건 }
  
  {i:i**2 for i in range(5)}              # {0:0, 1:1, 2:4, 3:9, 4:16}
  {i:i**2 for i in ragne(5) if i%2 == 0}  # {0:0, 2:4, 4:16}
  
  # set comprehension
  { 표현식 for 변수 in 순회가능한객체 }
  { 표현식 for 변수 in 순회가능한객체 if 필터링조건 }
  
  {i%5 for i in range(20)}                # {0, 1, 2, 3, 4}
  {i%5 for i in range(20) if i%2==0}      # {0, 1, 2, 3, 4}
  ```

  

#### Generator Expression (제너레이터 표현식)

- 문법비교) list comprehension : 한번에 list를 생성

  ```python
  >>> [i**2 for i in range(100)]
  [0, 1, 4, 9, 16, 25, 36, 49, 64, ...]
  ```

- generator expression : 값을 그때그때 생성하여 yield

  ```python
  >>> (i**2 for i in range(100))
  <generator object <genexpr> at 0x00000294CECF18E0>
  ```

- 제너레이터 표현식으로 list / tuple 만들기

  ```python
  >>> list(i**2 for i in range(100))
  [0, 1, 4, 9, 16, 25, 36, 49, 64, ...]
  >>> tuple(i**2 for i in range(100))
  (0, 1, 4, 9, 16, 25, 36, 49, 64, ...)
  
  ```

  

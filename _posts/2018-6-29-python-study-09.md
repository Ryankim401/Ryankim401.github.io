---
categoreis: Python
title: Python Study 9
---

## Python study Ep09 순회 가능한(Iterable) 객체

### 참고) Iterables vs. Iterators vs. Generators

![img](https://nvie.com/img/relationships.png) 



*[출처: https://nvie.com/posts/iterators-vs-generators/]*

- Iterable : 순회 가능한 객체

- Generator : 값을 생산해내는 객체

  - generator expression : 제너레이터 표현식

  - generator function : 제너레이터 함수

    

------



- 컨테이너(Container)

  컨테이너(Cointainer)는 원소들을 가지고 있는 데이터 구조이며 멤버십 테스트를 지원한다. (멤버십 테스트는 아래에 나온다) 이는 메모리에 상주하는 데이터 구조로, 보통 모든 원소값을 메모리에 가지고 있다. Python에서 잘 알려진 컨테이너는 다음과 같다.

  - list, deque...
  - set, frozonset...
  - dict, defaultdict, OrderedDict, Counter...
  - Tuple, nametuple...
  - str

  컨테이너는 실세계의 컨테이너(박스, 컵보드, 집 화물 등)처럼 생각하면 된다.

  기술적으로, 어떤 객체가 특정한 원소를 포함하고 있는지 아닌지를 판단할 수 있으며 컨테이너 라고 한다. 다음과 같이 리스트, 셋 또는 튜플에 대해 멤버십 테스트를 할 수 있다.

  ```python
  >>> assert 1 in [1, 2, 3]         # lists
  >>> assert 4 not in [1, 2, 3]
  >>> assert 1 in {1, 2, 3}         # sets
  >>> assert 4 not in {1, 2, 3}
  >>> assert 1 in (1, 2, 3)         # tuples
  >>> assert 4 not in (1, 2, 3)
  ```

  딕셔너리 멤버십은 키 값을 체크한다.

  ```python
  >>> d = {1: 'foo', 2: 'bar', 3: 'qux'}
  >>> assert 1 in d
  >>> assert 4 not in d
  >>> assert 'foo' not in d  # 'foo'는 딕셔너리의 키 값이 아니다
  ```

  마지막으로 문자열에는 부분문자열이 "포함"되어 있는지를 체크할 수 있다.

  ```python
  >>> s = 'foobar'
  >>> assert 'b' in s
  >>> assert 'x' not in s
  >>> assert 'foo' in s   # 문자열은 부분문자열을 모두 "포함"하고 있다.
  ```

  

- 이터레이블(Iterable)

- 이터레이터(Iterator)

- 제너레이터(Generator)

- 제너레이터 표현식(Generator expression)

- {list, set, dict} 컴프리헨션 ({list, set, dict} comprehension)

*[출처 https://mingrammer.com]*



### Generator 맛보기

```python
# a generator expression
>>> (i ** 2 for i in ragne(10))
<generator object <genexpr> at 0x0000013D2474C8E0>

# generator expression 으로 list 생성
>>> list(i**2 for i in range(10))
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# a generator function
def power():
    for i in range(10):
        yield i ** 2    # 함수 내에서 return 대신에 yield. yield시마다 값을 생산
       
power()
<generator object power at 0x0000013D22EA7258>

list(power())
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

```



### 순회 가능한 (Iterable) 객체

- set, list, dict, tuple, string, generator 는 모두 순회 가능한 객체

- Custom 클래스에 대해서도 순회가능토록 만들 수 있다.

  - \__iter__ 멤버함수 구현 : self가 iterator로서 동작을 하기 위해 self를 반환
  - \__next__ 멤버함수 구현 : iterator로서 동작

- for in 구문에서 활용가능

  ```python
  for ch in "hello world":
      print(ch)      # 글자 별로 조회
  for i in [1, 2, 3]:
      print(i)       # 숫자 별로 조회
  ```

  

### 사전(dict)의 경우

mydict = {'a': 1, 'b': 2} 

```python
for key in mydict:                      # key 별로 순회
    print(key,mydict[key])
    
for key in mydict.keys():               # key 별로 순회
    print(key, mydict[key])
    
for value in mydict.values():           # vlaue 별로 순회
    print(value) 
    
for (key, value) in mydict.item():      # (key, value) 쌍으로 순회
    print(key, value)
```



### 클래스를 통한 Iterable  객체 만들기

```python
class MyRange:
    def __init__ (self, start, end):
        self.start = start
        self.end = end
        
    def __iter__(self):
        return self             # iterator를 요구받고, 현 instance에서 next처리
    
    def __next__(self):
        if self.start >= self.end:
            raise StopIteration # 남은 요소가 없을 때, StopIteration 강제 발생
        value = self.start
        self.start += 1
        return value            # 다음 요소를 return
    
>>> iterable = MyRange(0, 3)

# objecct가 iterator가 아닐 경우, iterator(반복자)를 요구받음 - 인스턴스일 경우 __iter__ 호출
# for 루프를 돌며, iterator에 다음 요소를 요구 - 인스턴스일 경우 __next__ 호출
>>> for i in iterable:
        print(i)
0
1
2
```








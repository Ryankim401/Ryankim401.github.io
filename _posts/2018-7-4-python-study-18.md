---
categories: Python
title: Python Study 18
---

## Python Study Ep18 장식자

### 장식자(Decorator)

- 어떤 함수를 감싸는 (Wrapping) 목적의 함수

- 1급함수 : 함수를 동적으로 생성 가능, 반환값으로 전달 가능

  (함수를 변수처럼 취급 가능)

  ```python
  def base_10(fn):
      def wrap(x, y):
          return fn(x, y) + 10
      return wrap
  
  def mysum(x, y):
      return x + y                #  → @base_10
  mysum = base_10(mysum)
  
  >>> mysum(1, 2)
  13
  ```

  ```python
  @base_10
  def mysum(x, y):
      return x + y
  
  >>> mysum(1, 2)
  13
  ```



### 장식자에 인자 지원

```python
def base(base_i):
    def outer(fn):
        def wrap(x, y):
            return x + y + base_i
        return wrap
    return outer

@base(20)
def mysum2(x, y):
    return x + y

@base(30)
def mysum3(x, y, z):
    return x + y + z

>>> mysum2(1, 2)
>>> mysum3(1, 2, 3)

```



### Quiz: 지정된 조건의 인자만 처리하기

- filter_fn을 통과하지 못하는 인자는 alter_value 값으로 대체하기

  ```python
  def myfilter(filter_fn, alter_value):
      def wrap(fn):
          def inner(*args):
              raise NotImplementedError('구현해주세요.')  # TODO
          return inner
      return wrap
      
  @myfilter(lambda i : i%2==0, 0)
  def mysum(a, b, c, d, e):
      return a + b + c + d + e
  
  @myfilter(lambda i: i%2==0, 1)
  def mymultiply(a, b, c, d, e):
      return a + b + c + d + e
  
  >>> mysum(1, 2, 3, 4, 5)
  >>> mymultiply(1, 2, 3, 4, 5)
  ```

  

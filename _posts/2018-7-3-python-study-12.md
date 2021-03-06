---
categories: Python
title: Python Study 12
---

## Python Study Ep12 모듈, 패키지

### Agenda

- imput
- modules (모듈)
- packages (패키지)



### import

- 다른 파이썬 소스파일 내 함수/클래스 등을 현재의 공간으로 가져오기

- import 시점에서 해당 코드가 실행된다.

  module.py

  ├──  \__init__.py

  └── pkg2

  ​         └── \__init__.py

  ```python
  import module                 # module.py
  module.some_fn()              # module.py 내 some_fn
  
  from module import some_fn    # module.py 내 some_fn
  some_fn()
  
  import pkg1                   # pkg1/__init__.py
  import pkg1.pkg2              # pkg1/pkg2/__init__.py
  pkg1.pkg2.some_fn()           # pkg1/pkg2/__init__.py 내 some_fn
  
  from pkg1 import pkg2         # pkg1/pkg2/__init__.py
  pkg2.some_fn()
  ```

  ```python
  import mymodule1              # mymodule1.py 내 사항을 가져옴
  mymodule1.mysum(1,2)          # mymodule1.py 내 mysum 함수
  
  import pkg1.pkg2              # pkg1/pkg2/__init__.py 사항을 가져옴
  pkg1.pkg2.mysum(1,2)          # pkg1/pkg2/__init__.py 내 mysum 함수
  
  import pkg1.pkg2.모듈         # pkg1/pkg2/모듈.py 내 사항을 가져옴
  pkg1.pkg2.모듈.mysom(1,2)     # pkg1/pkg2/모듈.py 내 mysum 함수
  ```



### module (모듈)

- 다수의 함수 / 클래스들을 정의해둔 Python 소스코드 **파일**

  ```python
  # mymodule.py
  def mysum(x, y):
      return x + y
  mymultiply = lambda x, y: x * y
  ```

  실행

  ```python
  >>> import mymodule
  >>> mymodule.mysum(1, 2)
  3
  >>> mymodule.mymultiply(1, 2)
  2
  
  >>> from mymodule import mysuium, mymultiply
  >>> mysum(1, 2)
  >>> mymultiply(1, 2)
  ```



### package (패키지)

- Python 소스코드가 들어있는 **디렉토리**

- 해당 디렉토리에는 필이 \__init__ 파일이 있어야, Python 패키지로서 인식한다.

- 패키지를 import 할때에는 \__init__.py 가 import 대상이 된다.

  mylib

  ├─ \__init__.py

  ​        ├─ mysum4 임포트된 함수

  ├─ math.py

  ​        ├─ mysum4 함수

  ```python
  # mylib/__init__.py
  from .math import mysum4  # 현재 __init__.py 파일이 있는 디렉토리 내 math의 							 mysum4
  # mylib/math.py
  def mysum4(a, b, c, d):
      return a + b + c + d
  ```

  쉘에서 실행

  ```python
  # 가져와서 쓰기
  >>> from mylib import mysum4  # mylib/__init__.py 내 임포트된 mysum4 함수
  >>> mysum(1, 2, 3, 4)
  10
  >>> from mylib.math import mysum4 # mylib/math.py 내 오리지날 mysum4 함수
  >>> mysum(1, 2, 3, 4)
  10
  ```



### import 해서, 이름을 변경해서 쓰기

mylib.py

   ├─ mysum4 함수

mylib2.py

   ├─ mysum4 함수

```python
>>> from mylib import mysum4
>>> from mylib2 import mysum4  # 앞서 import된 mysum4를 덮어쓴다
>>> mysum4(1, 2, 3, 4)         # 둘 다 따로 쓰고싶은데, 늦게 import된 									   mylib2.mysum4만 사용된다
10
>>> mysum4(1, 2, 3, 4)
10
```

import 시에 as를 통해 원하는 이름으로 변경

```python
>>> from mylib import mysum4 as mylib_mysum4
>>> from mylib2 import mysum4 as mylib2_mysum4
>>> mylib_mysum4(1, 2, 3, 4)
10
>>> mylib2_mysum4(1, 2, 3, 4)
10
```



### Relative Import

패키지 내에서 다른 모듈 / 패키지 가져오기

main.py

pkg1

  ├─ \__init__.py

​          ├─ mysum 임포트된 함수

  ├─ math.py

​          ├─ mysum 함수

```python
# pkg1/math.py
def mysum(x, y):
    return x + y
# pkg1/__init_.py
from .math import mysum  # mysum 함수를 현재 이름공간(name)으로 가져옴

# main.py : 아래 2가지 mysum을 모두 사용 가능
from pkg1 import mysum
from pkg1.math import mysum

```



### import 경로

- import를 수행할 때, **sys.path** 경로에서 모듈 / 패키지 탐색
  - 환경변수 **PATH** 개념과 유사
- sys.path 는 **list**이기 때문에, 자유롭게 추가 / 수정 / 삭제 가능
  - 수정된 내용은 현재 프로세스에서만 유효
  - 관리성이 나빠지기 때문에 권장하는 방법은 아님
- 현재 디렉토리와 sys.path 경로에서 지정 모듈 / 패키지를 찾지 못했을 경우, ImportError 발생



### Python 소스코드 내 \__file__

- 해당 Python 소스코드 파일 경로

- pkg1/helloworld.py 일 경우

  - "/user/yanguk/desktop/study/pkg1/helloworld.py"
  - 참고 : 장고프로젝트/settings.py 내 BASE_DIR

  ```python
  from os.path import abspath, dirname
  BASE_DIR = dirname(dirname(abspath(__file__))) # 현 장고프로젝트 ROOT 절대											  경로 계산
  ```



### Python 소스코드 내 \__name__

- 해당 파이썬 소스코드 파일명

  - pkg1/helloworld.py 일 경우 : "helloworld"

- 비교

  - 최초 진입 소스코드일 경우 : "\__main__"으로 변경되어 실행
  - import 된 소스코드 : 본래 \__name__ 이 유지된 채로 실행

- 이를 통해, import시에는 실행되지 않고, **최초 진입 시**에만 실행될 코드를 지정 가능

  ```python
  def main():
      print('본 스크립트가 최초 진입 소스코드 경우에만 실행됩니다.')
      
  if __name__ == '__name__':
      main()
  ```

- 위 스크립트에서 if \__name__ == '\_\_main__' 블럭은 다른 소스코드에 의해 import 될 때에는 실행되지 않는다.

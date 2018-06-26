---
categories: Python
title: Python Study 1
---

## Python study Ep01 시작환경 구축하기

### 1. Python 프로그램 설치

- #### Python 설치 (Anaconda Python 추천)

- #### 소스코드 편집기 설치 (Visual Studio Code 윈도우추천, Atom, Sublime Text 3)

- #### IPython Notebook 설치 (Anaconda Python 포함됨)

  *기본 Python 설치방법 : 명령프롬프트(터미널) > pip3 install "ipython[notebook]"

  ```
  *맥 Permission Error 발생시 > **sudo** pip3 install "ipython[notebook]"
  ```

​          *(암호 : 맥 로그인 암호)

### 2. Python 코드실행 방법

- #### Interactive Shell 에서 실행하기 : python, ipython, jupyter notebook

  ```python
  > python
  >>> print(sum(range(101)))
  >>> exit()
  >
  ```

- #### Python Interpreter 실행시에 코드넣기

  ```python
  > python -c "print(sum(range(101)))"
  >
  ```

- #### 소스파일로부터 한 번에 실행하기

  ```python
  > pythone filename.py
  >
  ```

  visual studio code

  - 파일 - 폴더열기 - 현재디렉토리 새파일 생성

  - ![1529738420575](C:\Users\YANGUK\desktop\study\github\img\Ep01_1.png)

    *(코드 입력 후 항상 저장을 해야한다.)*

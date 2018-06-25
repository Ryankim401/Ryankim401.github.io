---
layout: post
title: Python Study 4
---

## Python study Ep04 블록문(Block Statement)

- 블록문(Block Statement) : 연속된 코드의 묶음
- 코드는 다수의 블록문으로 구성. 블록문 안에 다수의 블록문 중첩
- 블록 구분 : 들여쓰기(Indent), 다른 언어에서는 중괄호({})

  예1) Python

    ```python
    for i in range(4);
	    print(i)
    (공백 4칸)
	    1 
	    2
	    3
	    4
    ```

    예2) C

    ```c
    for(int i=0; i<4; i++) {
        print()
    }
    ```

### 들여쓰기(Indentation)

- 들여쓰기는 Tabs 또는 Spaces로 입력
  - Github 코드 저장소에서의 Tabs/Spaces 사용 통계
- 파이썬 언어 특징 중에서 가장 **호불호**가 갈리는 기능
  - 코드의 가독성 증대
- 하나의 들여쓰기는 <u>Python Style Guide #Indentation</u> 에 따라, **공백 4칸**을 권장

    **C코드.** 들여쓰기가 없어도 중괄호를 통해 블록 구분 가능

    ```c
    #include<stdio.h>

    int main() {
    int max = 10;
    int result = 0;
    for(int i=0; i<=max; i++){
    result = result + i;
    }
    printf("result = %d\n", result);
    return 0;
    }
    ```

    **PHP 코드.** 들여쓰기가 없어도 중괄호를 통해 블록 구분 가능

    ```php
    <?
    $max = 10;
    $result = 0;
    for ($i=0; $i<=$max; $i++){
    $result = $result + $i;
    }
    echo "result - $result";
    ?>    
    ```

    **JavaScript 코드.** 들여쓰기가 없어도 중괄호를 통해 블록 구분 가능

    ```javascript
    var max = 10;
    var result = 0;
    for(var i=0; i<=max, i++){
        result = result + i;
    }
    console.log("result = %s", result);
    ```

    **Python 코드**

    ```python
    max = 10;
    result = 0;
    for i in range(max+1):
        result = result + i      # 들여쓰기(Indentation) 강제
    print("result = %d" % result)
    ```

    **IndentationError**

    - 일관된 들여쓰기를 지키지 않는다면 IndentationError 발생
    - Tab과 Space는 엄연히 다른 글자입니다.

    ```python
    max = 10
    result = 0
    for i in range(max+1):
    result = result + i           # 들여쓰기(Indentation) 빠졌음
    Print("result = %d" % result)
    ```

    **탭>스페이스, 자동변환 기능**

    - 요즘 대개의 소스코드 편집기에서 자동변환 기능을 제공
    - Visual Studio Code : 디폴트 활성화
    - Sublime Text 3 : 아래 설정이 필요

    ```
    {
        "tab_size"; 4,
        "translate_tabs_to+spaces": ture
    }
    ```

### 주석(Comments)

- 소스코드는 설명하기 위한 목적
- 주석으로 쓴 부분은 실행되지 않습니다. 
- 파이썬에서의 주석 문법은 "1줄 주석"문법만 지원
  - "여러 줄 주석" 문법은 "문자열"로서 표기

    ```python
    # 주석1
    # 주석2
    ```

    ```
    ​	'문자열이지만, 주석처럼 쓰기도 한다'

    ​	' ' ' 이것도 문자열이지만, 

    ​	주석처럼 쓰기도 한다.' ' ' 
    ```

  **문자열은 주석이 아니다.**

    어디까지나 문자열일 뿐 주석이 아니다. 아래 코드는 SyntaxError가 발생

    ```python
    ' ' ' 설명설명
    ' ' '
    name = {
	    'Tom': 10,
	    'Steve': 12,
	    ' ' '
	    'John': 9,
	    'Anderson': 14,
	    'Bell': 8,
	    ' ' '
    }

    def mysun(a,b,c):
        ' ' '세 인자를 받아서, 더한 값을 리턴해준다
        ' ' '
        return a + b + c

    mysum?
    mysum.__doc__ (iPython이 아닌경우)
    ```

 *Docstring : 함수정의 시작하고나서 바로 쓰는것

 **PEP 8 : Style Guide for Python Code**

- PEP : Python Enhancements Proposals
- 일관성있는 코드 스타일을 위한 코드 스타일 제안
- 주요 스타일
  - 들여쓰기는 공백 4칸 (구글은 공백 2칸)
- 파이썬 코딩 컨벤션 by spoqa 

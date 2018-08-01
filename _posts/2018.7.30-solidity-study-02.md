---
categories: Solidity
title: Solidity Study 2
---
*이 게시글은 학습목적으로 작성되었으며 [블록체인 애플리케이션 개발 실전 입문] 책을 보면서 학습한 내용입니다.*

## 3장 스마트 계약 입문

### 3-1 스마트 계약 개요

#### 3.1.1 스마트 계약 개발

스마트 계약은 블록체인에서 동작하는 응용프로그램의 단위. 개발 흐름은 웹 응용 프로그램 개발과 동일.

개발자는 코드작성, 서버(블록체인)에 배포하고 사용자는 브라우저를 통해 서버에 접근하고, 목적한 일을 수행한다.

1. 개발자는 튜링 완전한 고급 언어로 계약 작성
2. 이를 EVM 컴파일러로 컴파일해 EVM 바이트코드(EVM 고유의 바이너리 형식)로 만들어 블록체인에 배포

EVM 바이트코드는 각 EVM에서 실행된다. (이것은 자바 프로그램, 자바 바이트코드, JVM의 관계와 비슷하다)

블록체인 네트워크에 참가하는 모든 노드는 같은 블록을 가지고 있기 때문에 모든 노드가 EVM 바이트코드를 보유하고 실행할 수 있다. 

![1533016119947](/home/ryan/Documents/markdown/image/smartcontract.png)

*출처 : 블록체인 애플리케이션 개발 실전 입문*

\* EVM : Ethereum Virtual Machine

\* 블록체인에 배포한다는 것은 블록 안에 EVM 바이트코드를 저장하는 것을 의미

계약(EVM 바이트코드)에 접근하는 것

사용자는 브라우저나 콘솔에서 블록체인에 존재하는 EVM 바이트코드에 JSON-RPC 등으로 접근한다. 

EVM 바이트코드는 연결한 노드의 EVM에서 실행되고 데이터를 갱신하는 경우(송금 등) 갱신 내용이 블록체인 네트워크에 전달된다

![1533016190086](/home/ryan/Documents/markdown/image/smartcontract2.png)

*출처 : 블록체인 애플리케이션 개발 실전 입문*

출처 : 블록체인 애플리케이션 개발 실전 입문



#### 3.1.2 스마트 계약 개발용 프로그래밍 언어

이더리움 계약을 만들기 위한 프로그래미 언어 세 가지

- Solidity

  Solidity는 자바스크립트와 문법이 유사한 언어로서, 현재 이더리움의 계약 개발에 가장 많이 사용되는 언어이며 가장 인기가 높다. 인터넷상의 정보도 많고 예제 코드도 풍부하다.

- Serpent

  Serpent는 파이썬 문법과 유사한 언어다. 인터넷상의 정보는 많지않지만 예측 시장에서의 블록체인 적용사례인 Auger Project는 Serpent를 이용하고 있다.

- LLL(Lisp Like Language)

  어셈블리와 유사한 저수준 언어로, 인터넷에도 거의 정보가 없다.



#### 3.1.3 컴파일러 설치

계약은 EVM 바이트코드로 컴파일한 뒤 블록체인에 배포해야하므로 Solidity의 컴파일러를 설치해야 한다.  우분투의 공식 리포지터리에서 배포되지 않았기 때문에 PPA(Personal Package Archive)를 사용해 설치한다.

다음 명령으로 PPA를 추가한 뒤 설치할 수 있다.

```shell
# 컴파일러 solc 설치
~$ sudo add-apt-repository ppa:ethereum/ethereum
~$ sudo apt-get update
~$ sudo apt-get install solc
# 버전확인
~$ solc --version
solc, the solidity compiler commandline interface
Version: 0.4.24+commit.e67f0147.Linux.g++
# 위치확인
~$ which solc
/usr/bin/solc
```

```shell
# Geth 실행하여 콘솔로 접속
~$ nohup geth --networkid 4649 --nodiscover --maxpeers 0 --datadir /home/ryan/data_testnet --mine --minerthreads 1 --rpc --rpcaddr "0.0.0.0" --rpcport 8545 --rpccorsdomain "*" --rpcapi "admin,db,eth,debug,miner,net,shh,txpool,personal,web3" --unlock 0,1 --password /home/ryan/data_testnet/passwd --verbosity 6 2>> /home/ryan/data_testnet/geth.log &nohup geth --networkid 4649 --nodiscover --maxpeers 0 --datadir /home/ryan/data_testnet --mine --minerthreads 1 --rpc --rpcaddr "0.0.0.0" --rpcport 8545 --rpccorsdomain "*" --rpcapi "admin,db,eth,debug,miner,net,shh,txpool,personal,web3" --unlock 0,1 --password /home/ryan/data_testnet/passwd --verbosity 6 2>> /home/ryan/data_testnet/geth.log &
[1] 4769
[2] 4770

~$ geth attach rpc:http://localhost:8545
Welcome to the Geth JavaScript console!

instance: Geth/v1.8.12-stable-37685930/linux-amd64/go1.10.1
coinbase: 0x039eb1db879ae8756b221945f102cff4ccc86b0e
at block: 4527 (Tue, 31 Jul 2018 15:04:18 KST)
 modules: eth:1.0 net:1.0 rpc:1.0 web3:1.0

```



------

##### alias로 geth 시작 명령어 등록

1. `alias`  확인

   ```shell
   ~$ alias
   alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'
   alias egrep='egrep --color=auto'
   alias fgrep='fgrep --color=auto'
   alias grep='grep --color=auto'
   alias l='ls -CF'
   alias la='ls -A'
   alias ll='ls -alF'
   alias ls='ls --color=auto'
   ```

2. `ll` 로 경로확인

   ```shell
   ~$ ll
   합계 224
   drwxr-xr-x 28 ryan ryan  4096  7월 31 15:36 ./
   drwxr-xr-x  3 root root  4096  7월 25 19:41 ../
   -rw-------  1 ryan ryan  4650  7월 31 13:55 .ICEauthority
   -rw-------  1 ryan ryan 13169  7월 31 15:18 .bash_history
   -rw-r--r--  1 ryan ryan   220  7월 25 19:41 .bash_logout
   -rw-r--r--  1 ryan ryan  4072  7월 31 15:36 .bashrc         # .bashrc 를 찾기위함
   drwx------ 24 ryan ryan  4096  7월 26 15:54 .cache/
   drwx------ 24 ryan ryan  4096  7월 27 14:06 .config/
   drwx------  3 ryan ryan  4096  7월 25 20:29 .dbus/
   drwxr-xr-x  2 ryan ryan  4096  7월 26 19:45 .ethash/
   drwx------  5 ryan ryan  4096  7월 31 15:33 .ethereum/
   --- 생략 ---
   ```

3. `vi .bash` 로 vi 편집기를 연다

   alias gethStartMineBackRPC(단축 명령어) = 'geth --networkid 4649 --nodiscover --maxpeers 0 --datadir /home/ryan/data_testnet --mine --minerthreads 1 --rpc --rpcaddr "0.0.0.0" --rpcport 8545 --rpccorsdomain "*" --rpcapi "admin,db,eth,debug,miner,net,shh,txpool,personal,web3" 2>> /home/ryan/data_testnet/geth.log &'

   추가하고 `:` `wq` 로 종료

   ![1533019579364](/home/ryan/Documents/markdown/image/alias.png)

4. `source .bashrc`로 적용

5. `alias` 확인 `gethStartMineBackRPC` 추가되었음

   ```shell
   ~$ alias
   alias alert='notify-send --urgency=low -i "$([ $? = 0 ] && echo terminal || echo error)" "$(history|tail -n1|sed -e '\''s/^\s*[0-9]\+\s*//;s/[;&|]\s*alert$//'\'')"'
   alias egrep='egrep --color=auto'
   alias fgrep='fgrep --color=auto'
   alias gethStartMineBackRPC='geth --networkid 4649 --nodiscover --maxpeers 0 --datadir /home/ryan/data_testnet --mine --minerthreads 1 --rpc --rpcaddr "0.0.0.0" --rpcport 8545 --rpccorsdomain "*" --rpcapi "admin,db,eth,debug,miner,net,shh,txpool,personal,web3" 2>> /home/ryan/data_testnet/geth.log &'
   alias grep='grep --color=auto'
   alias l='ls -CF'
   alias la='ls -A'
   alias ll='ls -alF'
   alias ls='ls --color=auto'
   ```

------



### 3-2 콘솔에서 계약 만들기

#### 3.2.1 Hello World

```js
pragma solidity ^0.4.8; // (1) 버전 프라그마

// (2) 계약 선언
contrac HelloWorld {
    // (3) 상태 변수 선언
    string public greeting;
    // (4) 생성자
    function HelloWorld(string _greeting) {
        greeting = _greeting;
    }
    // (5) 메서드 선언
    function setGreeting(string _greeting) {
        greeting = _greeting;
    }
    function say() constant returns(string) {
        return greeting;
    }
}
```

Solidity의 주석은 자바 등과 마찬가지로 행마다 주석을 다는 방법(행주석)과 영역을 지정해서 주석을 다는 방법(블록주석)이 있다. 행 주석은 해당 줄에서 `//` 뒤에 모든 글자를 주석으로 취급하는 것이고, 블록 주석은 `/*`와 `*/` 사이에 모든 내용을 주석으로 취급한다.

1. 버전 프라그마

   ```js
   pragma solidity ^0.4.8;
   ```

   컴파일러의 버전을 지정하는 명령이다. 호환성이 없는 컴파일러의 버전에서 컴파일할 수 없게 설정할 수 있다.

   초기 Solidity에서는 선언할 필요가 없었지만 현재는 반드시 선언해야 한다.

2. 계약 선언

```js
   contract HelloWorld {
   }
```

   contract로 계약을 선언한다. 계약은 자바 등 객체지향 프로그래밍 언어의 '클래스'와 매우 흡사하며 임의의 이름으로 만들 수 있다. 여기서는 HelloWorld라는 이름을 사용했다.

1. 상태 변수 선언

   ```js
   string public greeting;
   ```

   계약 내에서 유효한 변수를 선언할 수 있다. 이더리움에서는 이를 상태 변수라고 한다. 이 소스에서는 사용자로부터 전달된 문자열을 저장하는 변수 greeting을 선언했다. 여기서 public으로 되어있는 것에 주의해야 한다. public 변수는 그 계약에 접근할 수 있는 사용자라면 누구나 열람할 수 있다. 하지만 public 이라도 값을 변경할 수는 없다.

2. 생성자

   ```js
   function HelloWorld(string _greeting) {
       greeting = _greeting;
   }
   ```

   function으로 메서드를 선언한다. 생성자는 계약과 같은 이름을 가진 메서드로, 배포할 때만 실행 가능한 특별한 메서드이다. 여기서는 인수로 전달된 _greeting을 상태 변수에 설정했다. Solidity에서는 관례적으로 메서드의 인수 앞에 언더바를 붙인다.

3. 메서드 선언

   ```js
   function setGreeting(string _greeting) {
       greeting = _greeting;
   }
   function say() constant returns(string) {
       return greeting;
   }
   ```

   반환값을 돌려주는 메소드를 선언할 수 있다. 반환값을 돌려주는 경우 Returns의 괄호 안에 반환값의 데이터 형을 선언한다. 여기서 블록체인에 저장된 데이터의 변경을 수반하지 않는 경우 constant를 붙인다. 



#### 3.2.2 컴파일러 준비

컴파일하기에 앞서 소스 줄 바꿈을 제거해야 한다. (1) 우선 앞의 소스를 파일에 저장한다. (2) 그리고 `tr` 명령을 사용해 줄 바꿈을 모두 제거한다. 이때 행 주석은 삭제하거나 블록 주석으로 변경해야 한다. 파일은 임의의 위치에 생성해도 상관없다. 본인이 사용하기 편한 에디터를 사용해 앞의 소스를 HelloworldOrg.sol이라는 파일로 저장한다.

HelloWorldOrg.sol 파일의 내용

```shell
pragma solidity ^0.4.8;
contract Helloworld {
    string public greeting;
    function HelloWorld(string _greeting) {
        greeting = _greeting;        
    }
    function setGreeting(string _greeting) {
        greeting = _greeting;        
    }
    function say() constant returns(string) {
        return greeting;
    }
}
~$ cat HelloWorldOrg.sol | tr -d '\n' > HelloWorld.sol
~$ cat HelloWorld.sol
pragma solidity ^0.4.8;contract Helloworld {    string public greeting;    function HelloWorld(string _greeting) {        greeting = _greeting;            }    function setGreeting(string _greeting) {        greeting = _greeting;            }    function say() constant returns(string) {        return greeting;    }}
```



#### 3.2.3 컴파일 (이제 Geth로는 못한다)

#### 3.2.4 계약 배포



### 3-3 계약 개발 환경

#### 3.3.1 개발 환경

##### Browser-Solidity(Remix) https://remix.ethereum.org

Browser-Solidity는 Solidity 언어의 기여자(Contributor)가 개발한 Solidity 언어 전용 웹 브라우저 기반 IDE(통합 개발 환경)이다. 웹 브라우저에서 **계약 코드 작성**, **컴파일**, **이더리움 노드에 배포**, **계약 메서드의 실행** 등 일반적으로 필요한 작업을 수행할 수 있다. 이더리움 노드 없이 계약을 웹 브라우저의 자바스크립트 VM을 사용해 비슷하게 동작시킬 수도 있다.

##### Ethereum Studio https://live.ether.camp

리눅스의 이더리움 클라이언트 셸 접속도 가능한 cloud9 기반 웹 IDE이다. (사용자 등록 필요)

##### Intellij-Solidity https://plugins.jetbrains.com/plugin/9475-intellij-solidity

IntelliJ IDEA(및 기타 JetBrains IDE 전체)의 Solidity 플러그인이다.

##### Visual Studio Code Ethereum Solidity Extension http://github.com/juanfranblanco/vscode-solidity

마이크로소프트 비주얼 스튜디오 코드용 Solidity 플러그인이다.

##### Vim Solidity

구문 강조를 지원하는 Vim 에디터의 플러그인이다.

#### 3.3.2 Browser-Solidity 설치

Browser-Solidity를 이용하는 방법은 두 가지가 있다.

- 인터넷에 공개되어 있는 사이트 (https://remix.ethereum.org/)에 접속해 온라인으로 사용하는 방법
- Github에서 Zip파일을 내려받아 오프라인으로 이용하는 방법

Browser-Solidity는 Geth의 IP 주소와 포트 번호를 지정해 접속할 수 있다. 윈도우에 Browser-Solidity를 설치하고 원격(또는 가상머신)의 우분투에서 작동하는 Geth에 연결해 계약을 개발하는 것이 가능하다.



### 3-4 계약 개발

#### 3.4.1 Solidity 데이터 형식

```javascript
pragma solidity ^0.4.8;

contract DataTypeSample {
    function getValueType() constant returns (uint) {
        uint a;        // uint형 변수 a를 선언 이 시점에서는 a는 0으로 초기화 된다. 
        a = 1;         // a의 값이 1이 된다
        uint b = a;    // 변수 a에 a의 값 1이 대입
        b = 2;         // b의 값이 2가 된다.
        return a;
        }
    function getReferenceType() constant returns (uint[2]) {
        uint[2] a;     // uint 형식을 가진 배열 변수 a를 선언
        a[0] = 1;      // 배열의 첫 번째 요소의 값에 1을 대입.
        a[1] = 2;      // 배열의 두 번째 요소의 값에 2를 대입.
        uint[2] b = a; // uint 형식을 가진 배열 변수 b를 선언하고 a를 b에 대입. a는 데이터영역 
                       // 주소이기 때문에 b는 a와 동일한 데이터 영역을 참조함
        b[0] = 10;     // b와 a는 같은 데이터 영역을 참조하기 때문에 a[0]도 10이 된다.
        b[1] = 20;     // 마찬가지로 a[1]도 20이 된다
        return a;      // 10, 20이 반환된다.
    }
}   
```

pragma solidity ^0.4.8;

contract DataTypeSample {
    function getValueType() constant returns (uint) {
        uint a;        // uint형 변수 a를 선언 이 싲시점시점엣시점에선시점에서는 a는 0으로 초기화 된다. 
        a = 1;         // a의 값이 1이 된다
        uint b = a;    // 변수 a에 a의 값 1이 대입
        b = 2;         // b의 값이 2가 된다.
        return a;
        }
    function getReferenceType() constant returns (uint[2]) {
        uint[2] a;     // uint 형식을 가진 배열 변수 a를 선언
        a[0] = 1;      // 배열의 첫 번째 요소의 값에 1을 대입.
        a[1] = 2;      // 배열의 두 번째 요소의 값에 2를 대입.
        uint[2] b = a; // uint 형식을 가진 배열 변수 b를 선언하고 a를 b에 대입. a는 데이터영역 주소이기 때문에 b는 a와 동일한 데이터 영역을 참조함
        b[0] = 10;     // b와 a는 같은 데이터 영역을 참조하기 때문에 a[0]도 10이 된다.
        b[1] = 20;     // 마찬가지로 a[1]도 20이 된다
        return a;      // 10, 20이 반환된다.
    }
}   



Solidity에서 이용가능한 주 데이터 형식을 값 형식과 참조 형식으로 분류한 것

소수점(고정 및 부동) 을 다루는 데이터 형식은 구현되지 않는다. 날짜형 데이터 역시 존재하지 않는다.

------

No.	         	   논리명 			       				데이터형식		            값형식	                       참조형식

------

1			   불리언불리언(bool) 			       				bool                                     O                                -

2                         부호있는 정수              				int                                        O                                -

3                         부호없는 정수              				uint                                      O                                -

4                         주소                             				address                               O                                -

5                         배열(고정 길이, 가변 길이                    Arrays                                   -                                O

6                         문자열                                                  string                                    -                                O

7                         구조체                                                  Structs                                  -                                O

8                         매핑                                                      mapping                              -                                O

------



##### 불리언(bool)

불리언은 값으로 true, false 중 하나를 갖는 데이터 형식

비교연산자를 가진다. 초기값은 false

||, &&는 단락(short circuit) 연산으로 처리

if (f(x) || g(x)) {} 구문에서 f(x) = true 인 경우 g(x)는 실행되지 않는다.

if (f(x) && g(x)) {} 구문에서 f(x) = false 인 경우 g(x)는 실행되지 않는다.

------

연산자                               설명

------

!                                        논리부정

&&                                   논리곱 'and'

||                                    논리합 'or'

==                                    등식(같음)  

!=                                     부등식(같지 않음)

------



##### 정수(int, uint)

정수형은 다양한 크기를 가지며, 부호가 있는 형식(int)이 있고 부호가 없는 형식(uint : unsigned int)이 있다.

unit8 ~ unit256, int8 ~ int256 까지 8의 배수 길이로 형태가 존재한다. 이 숫자는 비트 수를 표시하는데 uint8이라면 0~255가 된다. 초기값은 uint, int 모두 0이다. uint는 uint256의 별칭, int는 int256의 별칭이다.

------

연산자                               설명

------

비교(bool 값으로 평가)     <=, <, ==, !=, >=, >

비트 연산자                       &(AND), |(OR), ^(XOR), ~(NOT)

산술 연산자                       +, -, *, /, %(나머지), **(제곱), <<(왼쪽 시프트), >>(오른쪽 시프트)

​                                         여기서 나누기는 항상 나머지를 버린다. 단, 양쪽 모두 상수인 경우 나머지를 버리지 않는다. 

​                                         그리고 0으로 나누기 연산은 예외가 발생한다. x << y는 x\*2\*\*y, x >> y는 x/x\*\* y다. 

​                                         왼쪽 시프트는 *2, *2,,, 이고, 오른쪽 시프트는 *1/2, *1/2,,,이 된다

------

```javascript
pragma solidity ^0.4.8;

contract Intsample {
    function division() constant returns (uint) {
        uint a = 3;
        uint b = 2;
        uint c = a / b * 10;     // a / b의 결과는 1이다.
        return c;                // 10이 반환된다
    }
    function divisionLiterals() constant returns (uint) {
        uint c = 3 / 2 * 10;     // 상수이기 때문에 a / b의 나머지를 버리지 않는다. 즉 1.5가 된다.
        return c;                // 15가 반환된다.
    }
    function divisionByZero() constant returns (uint) {
        uint a = 3;
        uint c = a / 0;          // 컴파일은 되지만 실행 시 예외가 발생한다.
        return c;                // uint c = 3 / 0으로 하면 컴파일도 진행되지 않는다.
    }
    function shift() constant returns (uint[2]) {
        uint[2] a;
        a[0] = 16 << 2;          // 16 * 2 ** 2 = 64
        a[1] = 16 >> 2;          // 16 / 2 ** 2 = 4
        return a;                // 64, 4가 반환된다
    }
}
```



##### 주소(address)

주소형식은 EOA나 계약 등의 계정 주소를 저장한다. 크기는 20바이트로, 초기값은 0x0000000000000000000000000000000000000000 이다. 정수형과 같은 비교 연산자를 가진다. 주소 형식만의 메서드가 있다. transfer와 send는 모두 Ehter를 송금하는 메서드지만 실패했을 때의 동작에 차이가 있다. transfer는 실패 시 예외가 발생해 모든 처리를 없었던 것으로 돌려놓지만 send는 처리가 계속된다. send를 사용할 경우 반드시 되돌려 줄 값을 체크해놔야 한다. 가스를 지정해 송금하기 위해서는 call.value().gass()()를 사용한다. 그리고 Ether를 주고받을 때는 상대에게 보내는 것이 아니라, 상대가 인출하게 하는 방법도 검토하는 것이 좋다.

------

연산자                               설명

------

비고(book 값으로 평가)                               <=, <, ==, !=, >=, >

\<address>.balance                                   주소가 가진 Ether를 wei 단위로 반환한다. 반환값은 uint256이다

\<address>.transfer(uint256 amount)   주소에 Ether를 amount만큼 송금한다. 단위는 wei. 실패시 예외가 발생한다.

\<address>.send(uint256 amount)         주소에 Ether를 amount만큼 송금한다. 단위는 wei. 실패시 false를 반환한다.   

returns (bool)

\<address>.call.value(uint256 amount)  주소에 Ether를 amount만큼 송금한다. 단위는 wei. send, trasfer와 비교해 

.gas(uint256 val)() returns (bool)            더 낮은 수준으로 평가한다. gas 값을 지정할 수 있다. 실패시 false를 반환한다

------



```javascript
pragma solidity ^0.4.8;

contract AddressSample {
    // 이름 없는 함수(송금되면 실행된다) payalbe을 지정해 Ether를 받는 것이 가능
    function () payable {}
    function getBalance(address _target) constant returns (uint) {
        if (_target == address(0)) {        // _target이 0인 경우 계약 자신의 주소를 할당
            _target = this;
        }
        return _target.balance;             // 잔고 반환
    }
    // 이후, 송금 메서드를 실행하기 전 이 계약에 대해 송금해둬야 한다.
    // 인수로 지정된 주소에 transfer를 사용해 송금
    function send(address _to, uint _amount) {
        if (!_to.send(_amount)) {           // send를 사용할 경우 반환값을 체크해야 한다.
            throw;
        }
    }
    // 인수로 지정된 주소에 call을 사용해 송금
    function call(address _to, uint _amount) {
        if (!_to.call.value(_amount).gas(1000000)()) {     // call도 반환값을 체크해야 한다.
            throw;    
        }
    }
    // 인출 패턴(transfer)
    function withdraw() {
        address to = msg.sender;            // 메서드 실행자를 받는 사람으로 한다.
        to.transfer(this.balance);          // 전액 송금한다.
    }
    // 인출 패턴(call)
    function withdraw2() {
        address to = msg.sender;            // 메서드 실행자를 받는 사람으로 한다
        if (!to.call.value(this.balance).gas(1000000)()) {      // 전액 송금한다.
            throw;
        }
    }
}
```

Browser-solidity(0.4.13 버전) 부터 throw를 더 이상 사용하지 않기 때문에 revert(), require(), assert() 를 사용하라는 경고 발생

- require()
  - 사용자 입력 검증
  - 외부 계약으로부터의 응답 검증(require(external.send(amount))
  - 상태 변경 작업을 수행하기 전 상태를 확인
  - 일반적으로 함수의 시작 부분에 사용
- assert()
  - 오버플로우(overflow) / 언더플로우(underflow) 확인
  - 불변성 검사
  - 변경 후 계약 상태 검증
  - 부정한 조건 검사
  - 일반적으로 함수의 끝부분에 사용
- revert()
  - 실행을 취소하고 상태를 원래대로 되돌린다.



##### 배열(고정 길이, 가변 길이)

배열 종류에 상관없이 처리할 수 있다. 배열은 임의 형식을 지정할 수 있다. 사이즈 k, 형식 T인 고정 길이 배열은 T[k]와 같이 선언하고, 가변 길이 배열은 T[]와 같이 선언한다. 배열 인덱스는 0부터 시작한다.

------

속성, 메서드 등        설명

------

\<array>.length      배열의 길이 속성, 가변 길이 배열에서는 이 값을 조작해 배열의 길이를 변경할 수 있다. 

​                                현재의 길이보다 큰 요소에 접근해도 배열의 길이는 변하지 않는다.

\<array>.push(x)    가변 길이 배열의 가장 뒤에 요소를 추가하는 메서드다. 반환값은 새로운 배열 길이다.

------

```javascript
pragma solidity ^0.4.8;

contract ArraySample {
    uint[5] public fArray = [uint(10), 20, 30, 40, 50];     // 고정 길이 배열의 선언 및 초기화
    uint[] public dArray;                 // 가변 길이 배열 선언
    function getFixedArray() constant returns (uint[5]) {
        uint[5] storage a = fArray;       // 길이가 5인 고정 배열을 선언
        // 메서드 안에서는 이 형식을 초기화할 수 없다.
        // uint[5] b = [uint(1), 2, 3, 4, 5]
        for (uint i = 0; i < a.length; i++) {  // 초기화
            a[i] = i + 1;
        }
        return a;             // [1, 2, 3, 4, 5]를 반환
    }
    function getFixedArray2() constant returns (uint[5]) {
        uint[5] storage b = fArray;   // 상태 변수로 초기화
        return b;                     // [10, 20, 30, 40, 50]을 반환
    }
    function pushFixedArray(uint x) constant returns (uint) {
        // 다음은 컴파일 오류가 발생한다.
        // fArray.push(x);
        return fArray.length;
    }
    function pushDArray(uint x) returns (uint) {
        return dArray.push(x);     // 인수로 받은 요소들 추가하고 변경 후의 배열 길이를 반환
    }
    function getDArrayLength() returns (uint) {
        return dArray.length;      // 가변 길이 배열의 현재 크기를 반환
    }
}
```



##### 구조체

구조체를 정의할 때는 C언어와 마찬가지로 struct 키워드를 사용한다. 구조체는 배열 데이터 형식으로도 만들 수 있다.

```javascript
pragma solidity ^0.4.8;

contract StructSample {
    struct User {           // 구조체 선언 (c언어와 동일)
        address addr;
        string name;
    }
    User[] public userList;      // 구조체 배열도 선언할 수 있다.
    function addUser(string _name) returns (uint) {      // 사용자 추가
        uint id = userList.push(User({                   // 배열의 가장 마지막에 추가한다.
            addr: msg.sender,
            name: _name
        }));
        return (id - 1);
    }
    function addUser2(string _name) returns (uint) {     // 사용자 추가
        userList.length += 1;                            // 배열의 길이를 1만큼 증가시킨다.
        uint id = userList.length - 1;
        userList[id].addr = msg.sender;
        userList[id].name = _name;
        return id;
    }
    function editUser(uint _id, string _name) {
        if (userList.length <= _id ||                    // id가 배열의 길이 이상
           userList[_id].addr != msg.sender)             // 주소가 등록된 것과 다르다
        {
            throw;      // 예외처리
        }
        userList[_id].name = _name;
    }
    
    // 구조체는 직접 반환하지 않기 때문에 다음 메서드는 컴파일 오류가 발생한다.
    // function getUser(uint _id) constant returns (User) {
    //   return userList[_id];
    // }
    // 아래 메서드는 문제 없음
    function getUser(uint _id) constant returns (address, string) {
        return (userList[_id].addr, userList[_id].name);
    }
}
```



##### 매핑(mapping)

매핑 형식이란 연상 배열이다. 키와 값을 매핑시킬 수 있다. mapping(_KeyType => _ValueType)과 같이 선언한다. 매핑은 논리적으로 모든 키가 존재하는 것처럼 초기화되고, 값은 각 데이터 형식으로 초기값을 갖는다. 직접 값을 지정하는 것도 가능하다.

```javascript
pragma solidity ^0.4.8;

contract MappingSample {
    struct User {
        string name;
        uint age;
    }
    mapping(address=>User) public userList;    // value를 구조체(User)로 설정
    	function setUser(string _name, uint _age) {
    	userList[msg.sender].name = _name;     // key를 지정해 접근한다.
        userList[msg.sender].age = _age;
    }
    function getrUser() returns (string, uint) {
        User storage u = userList[msg.sender];
        return (u.name, u.age);
    }
}
```



##### Ether 단위

데이터 형식과는 다르지만 Solidity 에서는 상수 값의 뒤에 Ether 단위를 나타내는 문자열을 붙일 수 있다. 단위를 나타내는 문자열을 붙여 수치를 변환할 수 있다.

------

Ether Units              Wei Value               Wei

------

wei                            1 wei                       1

szabo                        10^12 wei              1,000,000,000,000

finney                        10^15 wei              1,000,000,000,000,000

ether                          10^18 wei              1,000,000,000,000,000,000

------

```javascript
pragma solidity ^0.4.8;

contract EtherUnitSample {
    function () payable {}                // Ether를 받는 메서드
    // getEther 실행 전에 이 계약에 1 ether를 송금해야 한다.
    function getEther() constant returns (uint _wei, uint _szabo, uint_finney, uint _ether){
        uint amount = this.balance;       // 1,000,000,000,000,000,000
        _wei = amount / 1 wei;            // 1,000,000,000,000,000,000
        _szabo = _wei / 1 szabo;          // 1,000,000
        _finney = _wei / 1 finney;        // 1,000
        _ether = _wei / 1 ether;          // 1
    }
}
```



##### 시간 단위

상수 값의 뒤에 시간 단위를 나타내는 문자열을 붙여준다. 최소 단위는 '초'이며 단위 변환이 가능하다.

------

시간 단위                        초                                단위

------

seconds                         1                                 1

minutes                         60                               60초

hours                             3600                           60분

days                               86400                         24시간

weeks                            604800                       7일

years                              31536000                  365일

------

```javascript
pragma solidity ^0.4.8;

contract TimeUnitSample {
    uint public startTime;    // 시작 시간
    // 시작
    function start() {  
        startTime = now;      // now는 block.timestamp의 별칭(Alias)
    }
    // 시작 시간으로부터 지정한 '분'만큼 경과했는지 확인(bool 형태로 반환)
    function minutesAfter(uint min) constant returns (bool) {
        if (startTime == 0) return false;    // 시작 전에는 false를 반환
        return ((now - startTime) / 1 minutes >= min);
    }
    // 경과한 '초'를 반환
    function getSeconds() constant returns (uint) {
        if (startTime == 0) return 0;     // 시작 전에는 0을 반환
        return (now -startTime);
    }
}
```



##### 블록 속성 등

기타 블록 번호나 타임스탬프 등은 전역 변수로 취급된다. (대표적인 전역변수)

------

전역변수                                                               데이터 형식                   설명

------

block.blockhash(uint blockNumber)              bytes32                       지정한 블록의 해시 값

block.coinbase                                                   address                       해당 블록의 채굴자 주소

block.number                                                     uint                              해당 블록의 번호

block.timestamp                                                uint                              해당 블록의 타임스탬프

msg.sender                                                         address                       송금자 주소(현재의 호출처)

msg.value                                                            uint                              송금액

now                                                                      uint                               block.timestamp의 별칭

------


#### 3.4.2 계약 상속

계약은 상속을 지원한다. 다음 예제는 계약 A와 그 하위 계약 B를 정의하고, 계약 C에서는 계약 A 형태의 가변 길이 배열에 new를 사용해 A와 B를 저장하고 재정의(Override)한 같은 이름의 메서드를 호출한다. 여기서 계약을 new로 생성했는데, new는 Gas의 사용량이 많으니 주의해야 한다. Browser-Solidity에서는 gas를 지정할 수 없기 때문에 동작 확인을 할 때는 Geth의 콘솔 또는 Browser-Solidity의 자바스크립트 VM모드에서 수행하는 것이 좋다.

```javascript
pragma solidity ^0.4.8;

contract A {
    uint public a;
    function setA(uint _a) {
        a = _a;
    }
    function getData() constant returns (uint) {
        return a;        // a를 그대로 반환
    }
}

contract B is A {    // B는 A의 하위 계약
    function getData() constant returns (uint) {
        return a * 10;      // a * 10 을 반환
    }
}

contract C {
    A[] internal c;        // 데이터 형식을 계약 A 형식의 가변 길이 배열로 설정해 c로 선언
    function makeContract() returns(uint, uint) {
        c.length = 2;      // c의 길이를 2로 설정
        A a = new A();     // 계약 A를 a로 생성
        a.setA(1);         // 1을 할당
        c[0] = a;          // 배열의 첫 번째 요소에 a를 대입
        B b = new B();     // 계약 B를 b로 생성
        b.setA(1);         // 마찬가지로 1을 할당
        c[1] = b;          // 배열의 두 번째 요소에 b를 대입
        return (c[0].getData(), c[1].getData());    // 계약 A와 B의 반환값을 출력
    }
}
```



#### 3.4.3 다른 계약의 메서드 실행

상속으로도 실행할 수 있지만 메서드 실행 대상의 계약 주소와 형태가 만들어졌다면 다른 계약의 메서드를 실행할 수 있다. 아래 예제에서는 계약 A와 계약 B를 따로 배포한다. 그리고 계약 B에 계약 A의 주소를 설정해 계약 B에서 계약 A의 메서드를 실행한다. 

```javascript
pragma solidity ^0.4.8;

contract A {
    uint public num = 10;    // 10으로 고정한다(public이기 때문에 외부에서 참조 가능)
    function getNum() constant returns (uint) {
        return num;
    }
}

contract B {
    A a = new A();
    address public addr;
    function setA(A _a) {   // 별도로 생성한 A의 주소를 설정한다.
        addr = _a;      // 주소에 저장
    }
    // 상태 변수num의 값을 직접 취득
    function aNum() constant returns (uint) {
        return a.num();
    }
    // 메서드로부터 num의 값을 취득
    function aGetNum() constant returns (uint) {
        return a.getNum();
    }
}
```

#### 3.4.4 계약 파기

계약은 파기할 수 있다. 파기할 때 해당 계약이 보유하고 있는 Ether는 지저한 주소로 송금된다. 파기 명령은 selfdestruct(address) 또는 suicide(address)다. 

```javascript
pragma solidity ^0.4.8;

contract SelfDestructSample {
    address public owner = msg.sender;   // 계약을 배포한 주소를 소유자로 한다.
    // 송금을 받는다(close() 뒤에 호출하면 송금도 할 수 없게 된다.)
    function () payable {}
    // 계약을 파기하는 메서드
    function close() {
        if (owner != msg.sender) throw;    // 보내는 사람이 소유자가 아닌 경우는 예외 처리
        selfdestruct(owner);               // 계약을 파기한다.
    }
    // 계약 잔고를 반환하는 메서드
    function Balance() constant returns (uint) {    // close() 뒤에 호출하면 오류 발생
        return this.balance;
    }
}
```

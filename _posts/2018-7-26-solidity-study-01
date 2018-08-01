---
categories: Solidity
title: Solidity Study 1
---
*이 게시글은 학습목적으로 작성되었으며 [블록체인 애플리케이션 개발 실전 입문] 책을 보면서 학습한 내용입니다.*

# 2장 이더리움

## 2-1 이더리움 개요

### 2.1.1 이더리움 클라이언트

Ethereum is a decentralized platform that runs smart contracts: applications that run exactly as programmed without any possibility of downtime, censorship, fraud or third party interference.

*ethereum.org*

이더리움이란 특별히 정해진 구현 방법을 말하는 것이 아니라 스마트 계약을 실행할 수 있는 플랫폼이다. 

### 2.1.2 네트워크

이더리움은 크게 2개의 네트워크로 분류할 수 있다.

- 라이브 네트워크

  전 세계의 노드가 참가하는 공개된 네트워크이다. 누구라도 참가해 블록체인에 접근할 수 있으며 트랜잭션을 보낼 수 있다. 블록체인에 참가하는 블록을 결정하는 합의 프로세스에도 참가할 수 있다. 

  네트워크 상태는 http://Ethstats.net, http://EtherNodes.com, http://Etherscan.io, http://etherchain.org에서 확인 가능하다

- 테스트 네트워크

  - Morden 테스트 넷 : 라이브 네트워크처럼 전 세계의 노드가 참가할 수 있는 네트워크
  - 사설 테스트넷(Local Private Test-net) : 자신의 노드 하나만 참가할 수 있는 네트워크

  \* 채굴로 획득한 Ether는 그 테스트 안에서만 사용할 수 있다. 

### 2.1.3 Ether

이더리움에 'Ether'라는 가상화폐가 구현되어 있다. 가상화폐로서 주고 받을 수 있고, 계약을 수행하는 수수료로 이용할 수 있다.

Ether의 단위는 'ether'이나 비트코인과 마찬가지로 더 작은 단위로 나눌 수 있다. 가장 작은 단위는 wei로 1ether는 10^18wei 이다.

------

단위                             	        	Wei 가치					Wei

------

wei                    				1 wei					1

Kwei(babbage)				10^3 wei				1,000

Mwei(lovelace)				10^6 wei				1,000,000

Gwei(shannon)				10^9 wei				1,000,000,000

microether(szabo)			10^12 wei				1,000,000,000,000

milliether(finney)				10^15 wei				1,000,000,000,000,000

ether                    				10^18 wei				1,000,000,000,000,000,000

------

### 2.1.4 Gas

Ether의 송금과 계약을 실행하기 위해서는 수수료로 Ether를 지불해야 한다. 이를 'Gas'라고 한다. 이더리움의 사용자는 사용한 컴퓨팅 자원의 대가로 채굴자(Miner)에게 Gas를 지불한다. 지불하는 Gas는 요구하는 자원의 양과 복잡성으로 결정되는 수수료(Gas Fee)와 현재 Gas의 가격(Gas Price)에 의해 결정된다.

- Gas Fee

  가스 수수료는 이더리움에서 요구하는 자원의 양과 복잡도에 따라 가치가 결정되는 수수료다. 단위는 Gas다.

- Gas Price

  가스 가격은 1Gas당 가격이고 단위는 wei/Gas다. Ether의 가격이 변동되면 실질적으로 동일한 가치를 얻을 수 있도록 변경된다. 채굴자는 가스 가격이 높은 트랜잭션부터 실행한다 (= 블록에서 가져온다). 

  http://etherscan.io/chart/gasprice에서 평균, 최대, 최소 가스 가격을 확인할 수 있다.

  Gas Limit 값은 트랜잭션을 실행할 때 설정할 수 있는 인수의 하나로, 그 트랜잭션의 처리에 드는 최대값을 정하는 것이다. 만약 처리를 할 때 Gas Limit을 넘게 된다면 그 이상은 처리하지 않고 실행 전 상태로 돌린다. 하지만 Gas는 채굴자에게 지불된다 그렇기 때문에 대량의 자원을 사용하는 경우에는 거기에 맞는 Gas Limit을 설정해야 한다. 반대로 계약 측에서 잘못이 있어도 지불할 Gas는 Gas Limit을 초과하지 않는다. 즉, Gas Limit이라는 것은 최대값만 설정할 뿐이며, 반드시 지불해야 하는 것은 아니다. 남은 Gas는 지불처로 돌아온다.

  

## 2-2 Geth 설치

우분투에서 설치하는 방법

Geth는 Go언어로 만들어진 클라이언트이다. 소스코드부터 빌드해야하기 때문에 먼저 Go 언어와 C 컴파일러 등을 설치해야 한다.

```shell
$ sudo apt-get install -y build-essential libgmp3-dev golang git tree
```

git 저장소에서 소스를 다운로드 한다. 

```shell
$ git clone https://github.com/ethereum/go-ethereum.git
$ cd go-ethereum/
```

make geth 명령으로 빌드한다

```shell
$ make geth
```

geth 버전을 확인한다. 

```shell
$ .build/bin/geth version
Geth
Version: 1.8.12-stable
Git Commit: 37685930d953bcbe023f9bc65b135a8d8b8f1488
Architecture: amd64
Protocol Versions: [63 62]
Network Id: 1
Go Version: go1.10.1
Operating System: linux
GOPATH=
GOROOT=/usr/lib/go-1.10
```

geth를 /usr/local/bin에 복사한다.

```shell
$ sudo cp /usr/bin/geth /usr/local/bin/
```

경로가 제대로 설정되어 있는지 확인한다.

```shell
$ which geth
/usr/local/bin/geth
```



## 2-3 테스트 네트워크에서 Geth 기동

로컬 테스트넷에서 Geth를 기동하기 위해 준비해야하는 2가지

- 데이터 디렉터리
- Genesis 파일

데이터 디렉터리 생성 (data_testnet)

```shell
$ mkdir /home/ryan/data_testnet
$ cd /home/ryan/data_testnet/
$ pwd
/home/ryan/data_testnet
```

Genesis 파일 생성

```shell
   # config 를 입력해야한다
{
    "config": {},
    "coinbase" : "0x0000000000000000000000000000000000000000",
    "difficulty" : "0x1",
    "extraData" : "0x00",
    "gasLimit" : "0x47e7c5",
    "nonce" : "0x0000000000000042",
    "mixhash" : "0x0000000000000000000000000000000000000000000000000000000000000000",
    "parentHash" : "0x0000000000000000000000000000000000000000000000000000000000000000",
    "timestamp" : "0x00",
    "alloc" : { }
}
```

이후 geth에 genesis.json 위치를 등록한다

```shell
$ geth --datadir /home/ryan/data_testnet init /home/ryan/data_testnet/genesis.json
```

geth를 실행시키면 개발환경 준비가 끝난다.

```shell
$ tree data_testnet 
```

![1532672009936](/home/ryan/Documents/markdown/image/geth.png)

Geth 실행

```shell
$ geth --networkid 4649 --nodiscover --maxpeers 0 --datadir /home/ryan/data_testnet console 2>> /home/ryan/data_testnet/geth.log
```

- --networkid 4649 

  네트워크 식별자 (정수). 0~3은 예약된 숫자이기 때문에 이 외의 정수를 사용해야 한다(0=Olympic(disused), 1=Frontier, 2=Morden(disused), 3=Ropsten) (default: 1).  여기서는 4649를 지정했다.

- nodiscover

  생성자의 노드를 다른 노드에서 검색할 수 ryan      5178  1979  0 14:26 pts/0    00:00:00 grep --color=auto geth없게 하는 옵션이다. 노드 추가는 수동으로 해야한다. 지정하지 않으면 동일한 Genesis 파일과 네트워크 ID를 가진 블록체인 네트워크에 생성자의 노드가 연결될 가능성이 있다.

- maxpeers 0

  생성자의 노드에 연결할 수 있는 노드의 수를 지정한다. 0을 지정하면 다른 노드와 연결하지 않는다.

- datadir /home/ryan/data_testnet

  데이터 디렉터리를 지정한다. 지정하지 않으면 기본 디렉터리를 사용한다. 디렉터리는 자신의 환경에 맞게 지정한다.

- console

  대화형 자바스크립트 콘솔을 기동한다.

- 2>> /home/ryan/data_testnet/geth.log

  로그 파일을 만들 때 사용할 옵션으로, 에러를 해당 경로의 파일에 저장한다. Geth가 아닌 리눅스 셸 명령이다.

정상 입력시 다음 메시지와 프롬프트(>) 표시된다

![1532672171627](/home/ryan/Documents/markdown/image/geth2.png)



## 2-4 테스트 네트워크에서 Ether 송금

### 2.4.1 계정생성

이더리움에는 두 가지 종류의 계정이 있다.

- EOA(Externally Owned Account)

  일반 사용자가 사용하는 계정으로 비밀키로 관리된다. Ether를 송금하거나 계약을 실행할 수 있다.

- Contract

  계약용 계정으로 계약을 블록체인에 배포할 때 만들어지는 계정으로 블록체인에 존재한다. 다른 계정으로부터 메시지를 수신해 코드를 실행하고 계정에 메시지를 보낼 수 있다.

Geth 콘솔에서 `personal.newAccount` 명령을 실행하면 EOA를 만들 수 있다.

```go
> personal.newAccount("pass0")         # 계정의 패스워드로서 영숫자, 기호를 사용한 문자열 지정 가능
"0x039eb1db879ae8756b221945f102cff4ccc86b0e"           # 생성된 계정의 주소
```

계정(EOA)는 `eth.accounts` 명령으로 확인할 수 있다. 

```go
> eth.accounts
```

추가 계정 생성

```go
> personal.newAccount("pass1")
"0x98f23bb3947fce54675cdb7ff60969b3563b76b7"
> eth.accounts
["0x039eb1db879ae8756b221945f102cff4ccc86b0e","0x98f23bb3947fce54675cdb7ff60969b3563b76b7"]
 // 각 계정은 eth.accounts[0], eth.accounts[1] 처럼 인덱스 형태로 지정해 확인할 수 있다.
> eth.accounts[0]
"0x039eb1db879ae8756b221945f102cff4ccc86b0e"
> eth.accounts[1]
"0x98f23bb3947fce54675cdb7ff60969b3563b76b7"
```

콘솔을 종료하면 ps 명령으로 Geth 프로세스가 동작하지 않는 것을 확인할 수 있다.

```shell
ryan@ryan:~$ ps -eaf | grep geth
ryan      5178  1979  0 14:26 pts/0    00:00:00 grep --color=auto geth
```

셸에서 geth 명령을 사용해 계정알 만들 수 있다.

```shell
ryan@ryan:~$ geth --datadir /home/ryan/data_testnet account new
Your new account is locked with a password. Please give a password. Do not forget this password.
Passpharase: (pass2 입력)
Repeat passphrase: (pass2 재입력)
Address: "0x2af6da2d00598361a52a8ed4429013939dc7895d"
```

```shell
ryan@ryan:~$ geth -datadir /home/ryan/data_testnet account list
INFO [07-30|14:33:09.119] Maximum peer count                       ETH=25 LES=0 total=25
Account #0: {039eb1db879ae8756b221945f102cff4ccc86b0e} keystore:///home/ryan/data_testnet/keystore/UTC--2018-07-26T10-22-53.716175635Z--039eb1db879ae8756b221945f102cff4ccc86b0e
Account #1: {98f23bb3947fce54675cdb7ff60969b3563b76b7} keystore:///home/ryan/data_testnet/keystore/UTC--2018-07-26T10-36-51.138731499Z--98f23bb3947fce54675cdb7ff60969b3563b76b7
Account #2: {2af6da2d00598361a52a8ed4429013939dc7895d} keystore:///home/ryan/data_testnet/keystore/UTC--2018-07-26T10-38-27.405692907Z--2af6da2d00598361a52a8ed4429013939dc7895d
```

tree 명령으로 데이터 디렉터리를 표시할 수 있다. keystore에 계정 정보가 추가된 것을 볼 수 있다.

![1532928946710](/home/ryan/Documents/markdown/image/geth3.png)



### 2.4.2 채굴

geth 구동

```shell
~$ geth --networkid 4649 --nodiscover --maxpeers 0 --datadir /home/ryan/data_testnet console 2>> /home/ryan/data_testnet/geth.log
```

송금을 위한 Ether를 얻기 위한 채굴을 한다. 이더리움에서 채굴에 성공했을 때 보상을 받는 계정을 Etherbase라고 한다. Etherbase에는 기본적으로 `eth.account[0]`이 설정된다. `eth.coinbase` 명령으로 Etherbase를 확인할 수 있다.

```go
> eth.coinbase
"0x039eb1db879ae8756b221945f102cff4ccc86b0e"
```

Etherbase는 miner.setEtherbase 명령으로 변경할 수 있다. (다시 0으로 돌려놓음)

```go
> miner.setEtherbase(eth.accounts[1])
true
> eth.coinbase
"0x98f23bb3947fce54675cdb7ff60969b3563b76b7"
```

잔고 확인은 `eth.getBalance` 명령으로 할 수 있다. 인수로는 계정의 주소를 전달한다. 현재 만들어진 계정은 아직 Ether를 소유하고 있지 않으므로 잔고는 모두 0으로 표시된다.

```go
> eth.getBalance(eth.accounts[0])
0
> eth.getBalance(eth.accounts[1])
0
> eth.getBalance(eth.accounts[2])
0
```

블록 수는 `eth.blockNumber` 명령으로 확인할 수 있다. 

```go
> eth.blockNumber
0
```

채굴은 `miner.start(thread_num)` 명령으로 개시한다. `thread_num`은 채굴할 때 사용할 쓰레드 수다 

```go
> miner.start(1)
null
```

첫번째 채굴에서는 DAG(Directed Acyclic Graph) 가 생성되기 때문에 채굴이 완료되기 전까지 시간이 필요하다. DAG는 채굴의 ASIC 내성을 위해 만들어지는 약 1GB 크기의 파일로, 30,000블록 마다 다시 만들어진다.

DAG 파일은 $(HOME)/.ethash/full-R(임의숫자)-(숫자) 형식으로 만들어진다. `tree .ethash/ 명령으로 DAG 파일명을 확인할 수 있다.

```shell
~$ tree .ethash/
.ethash/
├── full-R23-0000000000000000
└── full-R23-290decd9548b62a8
0 directories, 2 files
```

채굴되고 있는지는 `eth.mining` 명령으로 확인할 수 있다. `eth.hashrate` 명령으로 해시 속도, `eth.blockNumber` 명령으로 블록 길이를 확인할 수 있다. 채굴 중의 해시 속도는 1 이상의 값이 된다.

```go
> eth.mining
true
> eth.hashrate
0
> eth.blockNumber
1413
```

채굴 보상을 받는 계정인 Etherbase(eth.coinbase = eth.accounts[0]) 잔고를 확인해보자

```go
> eth.getBalance(eth.coinbase)
7.165000378e+21
> eth.getBalance(eth.accounts[0])
7.185000378e+21
```

이 명령으로 표시되는 숫자의 단위는 wei 다. wei 는 이더리움에서의 최소 단위로, 1 ether는 10^18 wei(=1,000,000,000,000,000,000 wei) 다. wei 를 ether 로 변환해서 확인해보자

```go
> web3.fromWei(eth.getBalance(eth.accounts[0]),"ether")
7560.000378
```

### 2.4.3 Ether 송금

`eth.accounts[0]`에서 `eth.accounts[1]`로 10ether를 송금해보자. 송금은 `sendTransaction` 명령으로 수행한다

```go
> eth.sendTransaction({from:eth.accounts[0], to:eth.accounts[1], value:web3.toWei(10,"ether")})
Error: authentication needed: password or unlock
    at web3.js:3143:20
    at web3.js:6347:15
    at web3.js:5081:36
    at <anonymous>:1:1
```

송금을 실행하면 오류가 발생한다. 트랜잭션의 발행은 유료이기 때문에 잘못된 실행을 방지하기 위해 언제나 잠금 상태이며, 사용할 때 잠금을 해제(Unlock)해야한다. personal.unlockAccount 명령으로 계정 잠금을 해제할 수 있다. 명령을 실행하면 계정의 암호를 물어보는데, 앞서 설정한 암호를 입력하면 잠시 후 true를 반환하여 계정 잠금이 해제된다.

```go
> personal.unlockAccount(eth.accounts[0])
Unlock account 0x039eb1db879ae8756b221945f102cff4ccc86b0e
Passphrase: (암호 입력)
true
> personal.unlockAccount(eth.accounts[0], "pass0")    // 인수에 암호를 입력할 수도 있다
true
> personal.unlockAccount(eth.accounts[0], "pass0", 0)  // 시간 연장 인수 추가입력 가능
true
```

계정 잠금해제 유효시간은 300초이다. 이 시간을 연장하는 인수도 추가로 입력할 수 있다.(초단위). 0을 입력하면 Geth 프로그램 종료되기 전까지 계정 잠금해제 상태를 유지한다.

sendTransaction 실행

```go
> eth.sendTransaction({from:eth.accounts[0], to:eth.accounts[1], value:web3.toWei(10,"ether")})
"0x95ad89007caeca075fa2c5aecc226b02cecb71f06b33bf4a042b8ea6a994faf1"
```

sendTransaction으로 트랜잭션을 발행해도 처리가 실행되지 않는다. 블록체인에서는 블록 안에 그 트랜잭션이 포함될 때 트랜잭션의 내용이 실행된다. 

트랜잭션 상태 확인. 트랜잭션 ID를 인수로 `eth.getTransaction` 명령 실행

```shell
> eth.getTransaction("0x95ad89007caeca075fa2c5aecc226b02cecb71f06b33bf4a042b8ea6a994faf1")
{
  blockHash: "0x18683e00974ab2cf949a18526584ef44ae07ad31a1ca8f1a78422816cdb0608e",
  blockNumber: null,
  from: "0x039eb1db879ae8756b221945f102cff4ccc86b0e",
  gas: 90000,
  gasPrice: 18000000000,
  hash: "0x95ad89007caeca075fa2c5aecc226b02cecb71f06b33bf4a042b8ea6a994faf1",
  input: "0x",
  nonce: 1,
  r: "0x70fa9ebdf354c55e68edb28f5edfac893fbfb2d0d34ad91376a7e6185f1ac75a",
  s: "0x6c6abb8d971e0d2c6bf36ffb3d64959312f3865458baf1931fe429874e39d438",
  to: "0x98f23bb3947fce54675cdb7ff60969b3563b76b7",
  transactionIndex: null,
  v: "0x1b",
  value: 10000000000000000000
}
```

`blockNumber`가 null 인 상태다. null은 블록에 포함되지 않았다는 것을 표시한다.

`eth.pendingTransactions` 명령으로 계류중인 트랜잭션을 확인할 수 있다.

```go
> eth.pendingTransaction
[{
  blockHash: null,
  blockNumber: null,
  from: "0x039eb1db879ae8756b221945f102cff4ccc86b0e",
  gas: 90000,
  gasPrice: 18000000000,
  hash: "0x95ad89007caeca075fa2c5aecc226b02cecb71f06b33bf4a042b8ea6a994faf1",
  input: "0x",
  nonce: 1,
  r: "0x70fa9ebdf354c55e68edb28f5edfac893fbfb2d0d34ad91376a7e6185f1ac75a",
  s: "0x6c6abb8d971e0d2c6bf36ffb3d64959312f3865458baf1931fe429874e39d438",
  to: "0x98f23bb3947fce54675cdb7ff60969b3563b76b7",
  transactionIndex: null,
  v: "0x1b",
  value: 10000000000000000000
}]
```

미처리된 트랜잭션을 처리하기 위해 채굴을 재개해 블록을 생성한다.

```go
> miner.start(1)
true
> eth.pendingTransaction
[]
> miner.stop()
true
> eth.blockNumber
2665
```

`eth.getTransaction` 명령으로 트랙잭션을 확인하면 null이었던 blockNumber에 숫자가 할당된 것을 확인할 수 있다.

```go
> eth.getTransaction("0x95ad89007caeca075fa2c5aecc226b02cecb71f06b33bf4a042b8ea6a994faf1")
{
  blockHash: "0x18683e00974ab2cf949a18526584ef44ae07ad31a1ca8f1a78422816cdb0608e",
  blockNumber: 2485,
  from: "0x039eb1db879ae8756b221945f102cff4ccc86b0e",
  gas: 90000,
  gasPrice: 18000000000,
  hash: "0x95ad89007caeca075fa2c5aecc226b02cecb71f06b33bf4a042b8ea6a994faf1",
  input: "0x",
  nonce: 1,
  r: "0x70fa9ebdf354c55e68edb28f5edfac893fbfb2d0d34ad91376a7e6185f1ac75a",
  s: "0x6c6abb8d971e0d2c6bf36ffb3d64959312f3865458baf1931fe429874e39d438",
  to: "0x98f23bb3947fce54675cdb7ff60969b3563b76b7",
  transactionIndex: 0,
  v: "0x1b",
  value: 10000000000000000000
}
```

`eth.getBlock` 명령으로 블록을 확인하면 transaction 항목에 앞의 트랜잭션 ID 값이 표시되는 것을 볼 수 있다.

```go
> eth.getBlock(2485)
{
  difficulty: 407991,
  extraData: "0xd88301080c846765746888676f312e31302e31856c696e7578",
  gasLimit: 4712388,
  gasUsed: 21000,
  hash: "0x18683e00974ab2cf949a18526584ef44ae07ad31a1ca8f1a78422816cdb0608e",
  logsBloom: "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  miner: "0x039eb1db879ae8756b221945f102cff4ccc86b0e",
  mixHash: "0x7950a62badbd4070d2e59cb26382046538fa2b9d1bbbf35e0f5d941c1b1c0154",
  nonce: "0x57274eb43c1d4388",
  number: 2485,
  parentHash: "0xb0e73a1a3bee25fbbac102b9398a66c3b3641717e6ec7494a10c00962f231f5c",
  receiptsRoot: "0x51331390bef5c8852d2dceb32ee3d72b5773b12ae1bf6d20facde082fb966cd9",
  sha3Uncles: "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
  size: 652,
  stateRoot: "0xd52340f4dcf8762c30877076690002e2579e61ec03bb5d8bbec51701e99be3d6",
  timestamp: 1532935691,
  totalDifficulty: 614655130,
  transactions: ["0x95ad89007caeca075fa2c5aecc226b02cecb71f06b33bf4a042b8ea6a994faf1"],
  transactionsRoot: "0xf6982e6c23f566556983064c3088617ca0e77a41cd64fd7b88b9120e03807e6b",
  uncles: []
}
```

eth.accounts[1] 잔고 확인

```go
> eth.getBalance(eth.accounts[1])
14999622000000000000
> web3.fromWei(eth.getBalance(eth.accounts[1]), "ether")
14.999622
```

### 2.4.4 트랙잰션 수수료

eth.accounts[1] 에서 eth.accounts[2]로 송금

```go
// eth.accounts[1] 잠금해제
> personal.unlockAccount(eth.accounts[1], "pass1", 0)
true
// eth.accoutns[1] 에서 eth.accounts[2] 로 송금
> eth.sendTransaction({from:eth.accounts[1], to:eth.accounts[2], value:web3.toWei(5, "ether")})
"0x080e34ae033fe9b6209834d087948f5e21260fd71a570bd08a025c468ea96c65"
// eth.accounts[2] 잔고확인
> eth.getBalance(eth.accounts[2])
5000000000000000000
> web3.fromWei(eth.getBalance(eth.accounts[2]), "ether")
5
// eth.accounts[1] 잔고확인
> eth.getBalance(eth.accounts[1])
4999244000000000000
> web3.fromWei(eth.getBalance(eth.accounts[1]), "ether")
4.999244
// 잔고가 부족한 이유는 수수료로 사용되었기 때문이다.
```

![1532948319032](/home/ryan/Documents/markdown/image/geth4.png)

gas : 지불 가능한 최대 Gas이며, 실제로 해당 트랜잭션을 처리하는데 지불한 Gas는 아니다. 

지불한 수수료 [wei] / gasPrice [wei/Gas] = 지불한 Gas 양

\* eth.accounts[0] 에서 eth.accounts[1] 로 송금할 때 수수료 차감이 안되는 이유는 eth.accounts[0] 은 Etherbase 이기 때문에 발생한 수수료를 돌려받기때문에 차감이 안되는 것처럼 보인다.

### 2.4.5 백그라운드로 Geth 기동

백그라운드에서 동작하며 채굴을 수행하도록 설정하는 방법

```shell
~$ nohup geth --networkid 4649 --nodiscover --maxpeers 0 --datadir /home/ryan/data_testnet/ --mine --minerthreads 1 --rpc 2 >> /home/ryan/data_testnet/geth.log &
[1] 389
~$ nohup: 입력을 무시하고 stderr를 stdout으로 redirecting
```

- nohup

  유닉스 계열 OS의 명령(Geth 옵션 아님). `SIGHUP`을 무씨한 상태로 프로세스를 가동한다. 셸로부터 `SIGHUP`이 전송되도 무시하기 때문에 로그아웃 후에도 프로세스가 종료되지 않는다. 중지하기 위해서는 `kill` 명령을 사용한다

- --mine

  채굴을 활성화한다

- --minerthreads 1

  채굴에 사용할 CPU 쓰레드 수를 지정한다. 기본값은 1이다.

- --rpc

  HTTP-RPC 서버를 활성화한다. 별도의 콘솔에 연결할 때 필요한 옵션이다. 

- &

  명령을 백그라운드에서 실행한다. 이 명령도 Geth 옵션은 아니다

다음 명령을 통해 Geth 콘솔에 접속할 수 있다.

```shell
~$ geth attach rpc:http://localhost:8545
Welcome to the Geth JavaScript console!

instance: Geth/v1.8.12-stable-37685930/linux-amd64/go1.10.1
coinbase: 0x039eb1db879ae8756b221945f102cff4ccc86b0e
at block: 4437 (Mon, 30 Jul 2018 20:21:30 KST)
 modules: eth:1.0 net:1.0 rpc:1.0 web3:1.0
```

`exit`로 Geth를 빠져나온 뒤에도 Geth는 종료되지 않는 것을 확인할 수 있다.

```shell
> exit
~$ ps -eaf | grep geth
ryan       389   378 99 20:13 pts/0    00:09:23 geth --networkid 4649 --nodiscover --maxpeers 0 --datadir /home/ryan/data_testnet/ --mine --minerthreads 1 --rpc 2
ryan       603   378  0 20:22 pts/0    00:00:00 grep --color=auto geth
```

Geth를 종료할 때는 `kill`명령을 사용한다. `ps` 명령으로 확인한 프로세스 ID를 지정해 `kill`명령을 실행한다.

```shell
~$ kill 389
~$ ps -eaf | grep geth
ryan      1003   378  0 20:30 pts/0    00:00:00 grep --color=auto geth
[1]+  완료                  nohup geth --networkid 4649 --nodiscover --maxpeers 0 --datadir /home/ryan/data_testnet/ --mine --minerthreads 1 --rpc 2 >> /home/ryan/data_testnet/geth.log
```



### 2.4.6 JSON-RPC

HTTP를 이용한 작업. Geth에는 JSON-RPC 서버 기능이 포함되어 있다. Geth 기동 시 HTTP-RPC 서버를 활성화해서 원격에서 각종 명령을 실행할 수 있다.

```shell
~$ nohup geth --networkid 4649 --nodiscover --maxpeers 0 --datadir /home/ryan/data_testnet/ --mine --minerthreads 1 --rpc --rpcaddr "0.0.0.0" --rpcport 8545 --rpccorsdomain "*" --rpcapi "admin,db,eth,debug,miner,net,shh,txpool,personal,web3" 2>> /home/ryan/data_testnet/geth.log &
[1] 1616
```

- --rpc

  HTTP-RPC 서버를 활성화한다.

- --rpcaddr "0.0.0.0"

  HTTP-RPC 서버의 수신 IP를 지정한다. 기본값은 "localhost"다. "0.0.0.0"을 지정하면 localhost 뿐만 아니라 어떤 인터페이스에 대해 접근해도 수신한다.

- --rpcport 8545

  HTTP-RPC 서버가 요청을 받기 위해 사용하는 포트를 지정한다. 기본 포트 번호는 8545다.

- --rpccorsdomain "*"

  자신의 노드에 RPC로 접속할 IP주소를 지정한다. 쉼표로 구분해 여러 개를 지정할 수 있다. "*"로 지정하면 모든 IP에서 접속을 허용한다.

- --rpcapi "admin,db,eth,debug,miner,net,shh,txpool,personal,web3"

  rpc를 하가할 명령을 지정한다. 쉼표로 구분해 여러 개를 지정할 수 있다. 기본값은 "eth, net, web3"이다.



`curl` 명령으로 Geth 명령어 실행. `--data` 옵션에 JSON-RPC 형식으로 명령을 전송한다. (여기서는 Geth를 설치한 우분투 가상 머신에서 실행하므로 요청을 받을 주소는 localhost:8545 이다.

계정 생성. "method"에 Geth 명령(personal.newAccount)에 해당하는 API인("personal_newAccount")를 입력하고 "params"에 패스워드를 지정한다. "id"에는 임의의 숫자를 지정한다. 응답과 연결할 때 사용하는 것으로 요청하는 쪽에서 결정한다. 여기서는 10으로 지정.



### 2.4.7 Geth 기동 시 계정 잠금 해제

Geth를 시작할 때 지정한 계정을 잠금 해제하는 방법 (보안상 매우 좋지 않다)

포어그라운드에서 실행한다. (암호 : pass0)

```shell
~$ geth --networkid 4949 --nodiscover --maxpeers 0 --datadir /home/ryan/data_testnet --mine --minerthreads 1 --rpc --rpcaddr "0.0.0.0" --rpcport 8545 --rpccorsdomain "*" --rpcapi "admin,db,eth,debug,miner,net,shh,txpool,personal,web3" --unlock 0 --verbosity 6 console 2>> /home/ryan/data_testnet/geth.log

Unlocking account 0 | Attempt 1/3
Passphrase: (암호임력)
Welcome to the Geth JavaScript console!

instance: Geth/v1.8.12-stable-37685930/linux-amd64/go1.10.1
coinbase: 0x039eb1db879ae8756b221945f102cff4ccc86b0e
at block: 4456 (Mon, 30 Jul 2018 20:24:42 KST)
 datadir: /home/ryan/data_testnet
 modules: admin:1.0 debug:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0 web3:1.0
```

- --unlock 0

  잠금 해제할 계정을 지정한다. 이번에는 eth.accounts[0]을 잠금 해제했으므로 0을 지정했다. 쉼표로 구분해서 여러개를 지정할 수 있다.

- --verbosity 6

  로그 출력 수준을 지정한다. 0=silent, 1=error, 2=warn, 3=info, 4=core, 5=debug, 6=detail 이며 기본값은 3이다. (여기서는 가장 상세한 내용을 출력하도록 6을 지정)

  eht.accounts[0] 에서 eth.accounts[1]로 송금.

  ```shell
  > web3.fromWei(eth.getBalance(eth.accounts[1]), "ether")
  9.999244
  > eth.sendTransaction({from:eth.accounts[0], to:eth.accounts[1], value:web3.toWei(10, "ether")})
  "0x5560c34d4f7f79f373c8eed5b7212d758172115b6aaa6131ea56a89e37299824"
  > web3.fromWei(eth.getBalance(eth.accounts[1]), "ether")
  19.999244
  ```

  계정의 패스워드를 파일에 저장한 뒤, 해당 파일을 인수로 사용해 Geth를 시작하는 것도 가능하다.

  우선 패스워드를 저장할 파일을 만든다.

  ```shell
  ~$ echo pass0 > /home/ryan/data_testnet/passwd
  ~$ cat ~/data_testnet/passwd
  pass0
  ```

- --passwd /home/ryan/data_testnet/passwd

  패스워드 파일을 지정한다.



위 옵션을 추가해 Geth를 실행하면 패스워드를 묻는 절차없이 바로 Geth 콘솔로 진입한다.

```shell
~$ geth --networkid 4949 --nodiscover --maxpeers 0 --datadir /home/ryan/data_testnet --mine --minerthreads 1 --rpc --rpcaddr "0.0.0.0" --rpcport 8545 --rpccorsdomain "*" --rpcapi "admin,db,eth,debug,miner,net,shh,txpool,personal,web3" --unlock 0 --password /home/ryan/data_testnet/passwd --verbosity 6 console 2>> /home/ryan/data_testnet/geth.log
Welcome to the Geth JavaScript console!

instance: Geth/v1.8.12-stable-37685930/linux-amd64/go1.10.1
coinbase: 0x039eb1db879ae8756b221945f102cff4ccc86b0e
at block: 4479 (Tue, 31 Jul 2018 11:56:47 KST)
 datadir: /home/ryan/data_testnet
 modules: admin:1.0 debug:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0 web3:1.0
```

Geth 실행 옵션에서 계정을 여러 개 지정한 경우에는 다음과같이 패스워드 파일에 행 단위로 패스워드를 입력한다.

그리고 실행옵션 (--unlock)에서 잠금 해제할 계정의 번호를 입력하고, 여러 개의 계정에 대해 잠금 해제를 하는 경우 쉼표(,) 로 각 계정을 구분한다

```shell
~$ echo pass1 >> /home/ryan/data_testnet/passwd
~$ cat ~/data_testnet/passwd
pass0
pass1
~$ geth --networkid 4949 --nodiscover --maxpeers 0 --datadir /home/ryan/data_testnet --mine --minerthreads 1 --rpc --rpcaddr "0.0.0.0" --rpcport 8545 --rpccorsdomain "*" --rpcapi "admin,db,eth,debug,miner,net,shh,txpool,personal,web3" --unlock 0,1 --password /home/ryan/data_testnet/passwd --verbosity 6 console 2>> /home/ryan/data_testnet/geth.log
Welcome to the Geth JavaScript console!

instance: Geth/v1.8.12-stable-37685930/linux-amd64/go1.10.1
coinbase: 0x039eb1db879ae8756b221945f102cff4ccc86b0e
at block: 4492 (Tue, 31 Jul 2018 12:02:47 KST)
 datadir: /home/ryan/data_testnet
 modules: admin:1.0 debug:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0 web3:1.0
```

백그라운드 실행할 때도 동일한 옵션을 사용할 수 있다. attach로 접속할 수 있다.

```shell
~$ nohup geth --networkid 4949 --nodiscover --maxpeers 0 --datadir /home/ryan/data_testnet --mine --minerthreads 1 --rpc --rpcaddr "0.0.0.0" --rpcport 8545 --rpccorsdomain "*" --rpcapi "admin,db,eth,debug,miner,net,shh,txpool,personal,web3" --unlock 0,1 --password /home/ryan/data_testnet/passwd --verbosity 6 2>> /home/ryan/data_testnet/geth.log &
[2] 17783
~$ geth attach rpc:http://localhost:8545
Welcome to the Geth JavaScript console!

instance: Geth/v1.8.12-stable-37685930/linux-amd64/go1.10.1
coinbase: 0x039eb1db879ae8756b221945f102cff4ccc86b0e
at block: 5840 (Wed, 01 Aug 2018 19:53:37 KST)
 datadir: /home/ryan/data_testnet
 modules: admin:1.0 debug:1.0 eth:1.0 miner:1.0 net:1.0 personal:1.0 rpc:1.0 txpool:1.0 web3:1.0
~$
```


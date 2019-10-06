---
layout: post
title:  "DailyStudy"
categories : DailyStudy!
date:   2019-08-22



---



## August.22.2019  (Thu)

### Learned Today 

1. Geth (Go-ethereum)  
   이더리움 프로토콜을 Go 언어로 구현한 풀 노드 클라이언트 프로그램  
   주요 기능  

   * 이더리움 네트워크 참여
   * 실제 이더 채굴
   * 사용자간 이더 전송
   * 스마트 컨트랙트 생성 및 배포
   * 블록 조회 및 검색

   

이더리움 네트워크  

* Main net
* Test net
* private

Genesis.json 으로 초기화 할 수 있다.

실습(p.161)

* genesis.json 파일 생성하기

```json
{
    "config": {
        "chainId": 5678,
        "homesteadBlock": 0,
        "eip155Block": 0,
        "eip158Block": 0
    },
    "nonce": "0x0000000000000042",
    "timestamp": "0x00",
    "parentHash":
    "0x0000000000000000000000000000000000000000000000000000000000000000",
    "extraData": "0x00",
    "gasLimit": "0x800000",
    "difficulty": "0x400",
    "mixhash": 
    "0x0000000000000000000000000000000000000000000000000000000000000000",
	"coinbase": "0x2222222222222222222222222222222222222222", //있어도 되고 없어도 되고
    "alloc": {} //초기 할당 코인
    

```



계좌 만들기  
`$ ./geth --datadir chaindata/ account`  
계좌초기화  
`$ ./geth --datadir chaindata init ./genesis.json`

`./geth --datadir chaindata --networkid 9583 console  
\> eth.accounts `  
et



postman 으로 http://localhost:8545 로 보내기

``` json
{
	"jsonrpc" :"2.0",
	"method" : "eth_blockNumber",
	"id" : 10
}
```

추후 웹과 geth를 연결해서 사용한다.

## August.22.2019  (Thu)

1. geth 실행 `>  geth --datadir chaindata --networkid 9583 --nodiscover --maxpeers 0 --rpc -rpcaddr "0.0.0.0" --rpcport 8545 --rpccorsdomain "*" --rpcapi "db,eth,net,web3,admin,debug,miner,shh,txpool,personal" console`

2. node i ---save web3 로 web3 설치

3. web3 를 위해 js파일 만들기  

   ```javascript
   var Web3 = require('web3');
   var web3 = new Web3('http://localhost:8545');
   
   // console.log(web3);
   
   web3.eth.getBlockNumber((err, number) => {
       console.log(number);
   });
   ```

4. node로 계정 생성  

   ```javascript
   
   ```

   

# **Todo List**

# **Term**


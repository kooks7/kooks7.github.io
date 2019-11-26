---
layout: post
title:  "DailyStudy(truffle)"
categories : DailyStudy!
date:   2019-09-06



---



## Learn Today

## 1. 트러플

**개요** 

**설치및 실행 **

` $ npm i -g truffle`  
`$ truffle init`  
`$ truffle compile`   

` truffle-config.js ` 파일에 네트워크 정보 수정

```javascript
   development: {
     host: "127.0.0.1",     // Localhost (default: none)
     port: 8545,            // Standard Ethereum port (default: none)
     network_id: "9583",       // Any network (default: none)
    },
```

`$ truffle migrations`



**develop 기능**

트러플을 개발할 수 있는 개발환경으로 콘솔이 바뀐다.

**새로운 프로젝트 metacoin**

`$ truffle upbox` => 새로운 프로젝트 예제 다운  
`truffle(develop)> compile`  
`truffle(develop)> migrate`  
`truffle(develop)> test` 

```json
truffle(develop)> let MyContract = await MetaCoin.deployed()
undefined
truffle(develop)> let bal = await MyContract.getBalance(accounts[0])
undefined
truffle(develop)> bal
<BN: 2710>
truffle(develop)>

// 1번 계좌로 송금
truffle(develop)> MyContract.sendCoin(accounts[1],500)
{ tx:
   '0x6447b4d8878ba7807d206aa61ba752ae6099f259196b62260a53df05ed368e0f',
  receipt:
   { transactionHash:
      '0x6447b4d8878ba7807d206aa61ba752ae6099f259196b62260a53df05ed368e0f',
     transactionIndex: 0,
     blockHash:
      '0xf984af26c5c96abc768145ea7de4be4116c1cb01adb1ec239ee25e7a23933efc',
     blockNumber: 12,
     from: '0x1c42afe5ee0959bfd163bb010136e80a1f6b086c',
     to: '0x1d9a44c46bd349353634b4a7d40412a25e80eb3c',
     gasUsed: 50923,
     cumulativeGasUsed: 50923,
     contractAddress: null,
     logs: [ [Object] ],
     status: true,
     logsBloom:
      '0x00002000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000010000000000000008000000000002000000000000000000000000000000000004000000000000000000040000000000000000000000000010000000000000000000000000000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000002000000000000000000000000000000001000000000000000000000000000000000000200000000000000000000000000000000000000000000000000',
     v: '0x1b',
     r:
      '0x3c28611a368e78168fa4e9f20f64ba2e93e68718e2d85a80f6ecdb62c14c0d4d',
     s:
      '0xda467ac399b3cd6f7c08d0a423703a0041c39aed20b36766e61094f705089dc',
     rawLogs: [ [Object] ] },
  logs:
   [ { logIndex: 0,
       transactionIndex: 0,
       transactionHash:
        '0x6447b4d8878ba7807d206aa61ba752ae6099f259196b62260a53df05ed368e0f',
       blockHash:
        '0xf984af26c5c96abc768145ea7de4be4116c1cb01adb1ec239ee25e7a23933efc',
       blockNumber: 12,
       address: '0x1d9A44c46bd349353634B4a7D40412A25E80EB3c',
       type: 'mined',
       id: 'log_a86162e4',
       event: 'Transfer',
       args: [Result] } ] }
```

> 교재 237~251 페이지 복습

### 2. 실습

`TestContract.sol` 생성

```javascript
pragma solidity ^0.5.8;

contract TestContract {
    string value;
    
    constructor() public {
    }
    
    // get 
    function getValue() public view returns (string memory){
        return value;
    }

    // set
    function setValue(string memory _value) public{
        value = _value;
    }    
}

```

`3_deploy_testcontract.js` 생성

```javascript
const TestContract = artifacts.require("TestContract");

module.exports = function(deployer) {
  deployer.deploy(TestContract); // 블록체인에 배포하는 함수
};

```

콘솔 창에 실행

`truffle(develop)>compile --all`  
`truffle(develop)> migrate --reset`  
`truffle(develop)> let metaCoin = await MetaCoin.deployed()` => metacoin에 배포  
`truffle(develop)> let bal = metaCoin.getBalance(accounts[0]) `  

**배포한 함수 실행하기**

` truffle(develop)> let testContract = await TestContract.deployed()`  
` truffle(develop)> testContract.setValue('Hello')` // set함수에 값 할당  
` truffle(develop)> testContract.getValue()` // 'Hello' 나옴!
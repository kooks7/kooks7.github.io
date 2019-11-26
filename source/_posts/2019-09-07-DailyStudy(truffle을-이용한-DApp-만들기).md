---
layout: post
title:  "DailyStudy(truffle을 이용한 DApp 만들기)"
categories : DailyStudy!
date:   2019-09-07

---



## Learn Today

## ERC20 토큰을 이용한  프로젝트

**ERC20 토큰**  
**ERC-20** is a technical standard used for smart contracts on the Ethereum blockchain for implementing tokens.  
-Wikipedia-

**코인과 토큰의 차이**  
코인: 블록체인 네트워크를 가지고 있으면 코인이라 한다.(Bitcoin, Ether )  
토큰: 독립적인 블록체인 네트워크를 소유하지 않은 경우 토큰이라 한다. (EOS)

**프로젝트 만들기**

새 디렉토리에

1. truffle unbox tutorialtoken // ERC20 표준
2. npm i --save openzeppelin-solidity
3. truffle.js 파일명 수정 => truffle-config.js
4. truffle develop 에서 compile & migrate
5. contracts/TutorialToken.sol 만들기

```javascript
pragma solidity ^0.5.8;
 
import "openzeppelin-solidity/contracts/token/ERC20/ERC20.sol";
import "openzeppelin-solidity/contracts/token/ERC20/ERC20Detailed.sol";
 
contract TutorialToken is ERC20Detailed, ERC20 {
   uint public initialSupply = 1000e18;
 
   constructor (string memory _name, string memory _symbol, uint8 _decimals, uint _initialSupply)
      ERC20Detailed(_name, _symbol, _decimals)  public
       {
           initialSupply = _initialSupply ** _decimals;
           _mint(msg.sender, initialSupply);
       }
}
 

```

6. migrations/2_deploy_tutorialtoken.js

```javascript
let TutorialToken = artifacts.require("./TutorialToken.sol");

const _name = "TutorialToken";
const _symbol = "TTK";
const _decimals = 18;
const _initialSupply = 10000;

module.exports = function(deployer) {
  deployer.deploy(TutorialToken, _name, _symbol, _decimals, _initialSupply);
};

```



7. 실행하기
   => npm run dev

**이체하기**

1. 계좌 주소 가져오기

```
truffle(develop)> accounts
[ '0x1c42AFE5eE0959Bfd163Bb010136e80a1f6b086C',
  '0xa6B555b241643E2521E6c8f90c8b1eF4a64aCC19',
  '0x7079250970328161030A064311745b0688867375',
  '0xEDD574C96c73F7706AC1ae49C10CC8dD2FF20e18',
  '0xb4b39f0D191D21478AefF6AA83Be8962D804DAb1',
  '0x091943Bea1415BE0369D28DF359eB06DA906B647',
  '0xb35977827Dd44681527caD84E49ff7f6FB7e9F48',
  '0xae9BCD5018a03f507bC8Ed75Da031816bb8Ee317',
  '0xC5D17e47EA4504e7e13504cc3E3e5e08E210f5D4',
  '0x362732B434182E9f1d2549d880960Facf3f48D2f' ]
  
```

2. 메타마스크 설치 

3. 가나슈 띄우기

4. 메타마스크에서 로컬호스트8545로 변경 후 가나슈에서 계좌 가져오기  

   > 참고: truffle의 `truffle-config.js` 파일의 포트번호는 이 곳으로 deploy를 한다는 뜻이다. 즉 그 포트에 가나슈가 있으면 가나슈 블록체인에 배포하고 geth 가 있다면 geth에 배포한다는 것이다.

   

5. truffle-conifg.js 포트 8545로 변경

6. src/js/app.js 수정

   ```javascript
   App = {
     web3Provider: null,
     contracts: {},
   
     init: function() {
       return App.initWeb3();
     },
   
     initWeb3: function() {
       // Initialize web3 and set the provider to the testRPC.
       // if (typeof web3 !== 'undefined') {
       //   console.log('web3 is already defined...');
       //   App.web3Provider = web3.currentProvider;
       //   web3 = new Web3(web3.currentProvider);
       // } else {
         // set the provider you want from Web3.providers
         console.log('web3 is not defined...')
         App.web3Provider = new Web3.providers.HttpProvider('http://127.0.0.1:8545');
         web3 = new Web3(App.web3Provider);
       // }
   
       return App.initContract();
     },
   
     initContract: function() {
       $.getJSON('TutorialToken.json', function(data) {
         // Get the necessary contract artifact file and instantiate it with truffle-contract.
         var TutorialTokenArtifact = data;
         App.contracts.TutorialToken = TruffleContract(TutorialTokenArtifact);
   
         // Set the provider for our contract.
         App.contracts.TutorialToken.setProvider(App.web3Provider);
   
         // Use our contract to retieve and mark the adopted pets.
         return App.getBalances();
       });
   
       return App.bindEvents();
     },
   
     bindEvents: function() {
       $(document).on('click', '#transferButton', App.handleTransfer);
     },
   
     handleTransfer: function(event) {
       event.preventDefault();
   
       var amount = parseInt($('#TTTransferAmount').val());
       var toAddress = $('#TTTransferAddress').val();
   
       console.log('Transfer ' + amount + ' TT to ' + toAddress);
   
       var tutorialTokenInstance;
   
       web3.eth.getAccounts(function(error, accounts) {
         if (error) {
           console.log(error);
         }
   
         var account = accounts[0];
   
         App.contracts.TutorialToken.deployed().then(function(instance) {
           tutorialTokenInstance = instance;
   
           return tutorialTokenInstance.transfer(toAddress, amount, {from: account, gas: 100000});
         }).then(function(result) {
           alert('Transfer Successful!');
           return App.getBalances();
         }).catch(function(err) {
           console.log(err.message);
         });
       });
     },
   
     getBalances: function() {
       console.log('Getting balances...');
   
       var tutorialTokenInstance;
   
       web3.eth.getAccounts(function(error, accounts) {
         console.log('accounts = ', accounts);
         if (error) {
           console.log(error);
         }
   
         var account = accounts[0];
   
         App.contracts.TutorialToken.deployed().then(function(instance) {
           tutorialTokenInstance = instance;
   
           return tutorialTokenInstance.balanceOf(account);
         }).then(function(result) {
           balance = result.c[0];
   
           $('#TTBalance').text(balance);
         }).catch(function(err) {
           console.log(err.message);
         });
       });
     }
   
   };
   
   $(function() {
     $(window).load(function() {
       App.init();
     });
   });
   
   ```

   


---
layout: post
title:  "DailyStudy"
categories : DailyStudy!
date:   2019-09-10



---



## 

## Learned Today 

## 

## Ethereum 예제 pet shop

1. truffle unbox pet-shop

2. cd pet-shop

3. truffle ubox pet-shop

4. truffle-config.js 파일 수정

   ```javascript
   module.exports = {
     // See <http://truffleframework.com/docs/advanced/configuration>
     // for more about customizing your Truffle configuration!
     networks: {
       development: {
         host: "127.0.0.1",
         port: 8545,
         network_id: "*" // Match any network id
       },
       develop: {
         port: 8545
       }
     }
   };
   
   ```

5. Contract (Adoption.sol)  

   - 컨트랙트 파일 생성

   ```javascript
   pragma solidity >=0.4.22 <0.6.0;
    
   contract Adoption {
      address[16] public adopters;
    
      function adopt(uint petId) public returns (uint) {
          require(petId >= 0 && petId <= 15);
          adopters[petId] = msg.sender;
          return petId;
      }
    
      // Retrieving the adopters
      function getAdopters() public view returns (address[16] memory) {
          return adopters;
      }
   }
   
   ```

6. Compile 및 migrate

7. app.js 파일 수정

   ```javascript
   App = {
     web3Provider: null,
     contracts: {},
   
     init: async function() {
       // Load pets.
       $.getJSON('../pets.json', function(data) {
         var petsRow = $('#petsRow');
         var petTemplate = $('#petTemplate');
   
         for (i = 0; i < data.length; i ++) {
           petTemplate.find('.panel-title').text(data[i].name);
           petTemplate.find('img').attr('src', data[i].picture);
           petTemplate.find('.pet-breed').text(data[i].breed);
           petTemplate.find('.pet-age').text(data[i].age);
           petTemplate.find('.pet-location').text(data[i].location);
           petTemplate.find('.btn-adopt').attr('data-id', data[i].id);
   
           petsRow.append(petTemplate.html());
         }
       });
   
       return await App.initWeb3();
     },
   
     initWeb3: function() {
       if (typeof web3 == 'undefined') {
         App.web3Provider = web3.currentProvider;
       } else {
         App.web3Provider = new Web3.providers.HttpProvider('http://localhost:8545')
       }
       webr = new Web3(App.web3Provider);
       
   
   
       return App.initContract();
     },
   
     initContract: function() {
       $.getJSON('Adoption.json', function(data){
         var AdoptionArtifact = data;
         App.contracts.Adoption = TruffleContract(AdoptionArtifact);
         
         App.contracts.Adoption.setProvider(App.web3Provider);
   
         return App.markAdopted();
       });
   
   
       return App.bindEvents();
     },
   
     bindEvents: function() {
       $(document).on('click', '.btn-adopt', App.handleAdopt);
     },
   
     markAdopted: function(adopters, account) {
       var adoptionInstance;
   
       App.contracts.Adoption.deployed().then(function(instance) {
         adoptionInstance = instance;
   
         return adoptionInstance.getAdopters.call();
       }).then(function(adopters) {
         for(i=0; i<adopters.length; i++){
           if(adopters[i] !== '0x0000000000000000000000000000000000000000'){
             $('.panel-pet').eq(i).find('button').text('Success').attr('disabled',true);        
           }
         }
       }).catch(function(err) {
         console.log(err.message);
       });
     },
   
     handleAdopt: function(event) {
       event.preventDefault();
   
       var petId = parseInt($(event.target).data('id'));
   
       var adoptionInstance;
   
       web3.eth.getAccounts(function(error, accounts) {
         if(error){
           console.log(error);
         }
   
         var account = accounts[0];
         console.log(account);
   
         App.contracts.Adoption.deployed().then(function(instance) {
           adoptionInstance = instance;
   
           return adoptionInstance.adopt(petId, {from: account});
         }).then(function(result) {
           
           return App.markAdopted();
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

8. truffle-conifg.js 수정

   ```javascript
   var HDWalletProvider = require("truffle-hdwallet-provider");
   require('dotenv').config();
    
   var infura_apikey = process.env.API_KEY;
   var mnemonic = process.env.MNEMONIC;
    
   console.log("infura_apikey = ", infura_apikey);
   console.log("mnemonic = ", mnemonic);
    
   module.exports = {
     networks: {
       development: {
         host: "localhost",
         port: 8545,
         network_id: "*" // Match any network id
       },
       ropsten: {
         provider: new HDWalletProvider(mnemonic, "https://ropsten.infura.io/"+infura_apikey),
         network_id: 3
       }
     }
   };
   ```

9. npm install --save truffle-hdwallet-provider

10. truffle migrate --reset --network ropsten

11. private key 숨기기

    * `.env` 로 옮기기

      ```json
      API_KEY="v3/~~~"
      MNEMONIC="cruise ~~~"
      ```

12. truffle-config.js

    ```javascript
    var HDWalletProvider = require("truffle-hdwallet-provider");
    require('dotenv').config();
     
    var infura_apikey = process.env.API_KEY;
    var mnemonic = process.env.MNEMONIC;
     
    //console.log("infura_apikey = ", infura_apikey);
    //console.log("mnemonic = ", mnemonic);
    ```

    


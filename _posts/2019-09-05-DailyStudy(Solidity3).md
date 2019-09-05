---
layout: post
title:  "DailyStudy(Solidity3)"
categories : DailyStudy!
date:   2019-09-05




---



## Learned Today 

## 1. 첫번 째 실습

스마트 컨트랙트 예제 

CrowdFunding.sol 파일 만들기

Node.js  콘솔에서 remix 연결하기

1. `var Web4 = require('web3');`
2. `var web3  = new Web3('http://localhost:8545');`

```javascript
abi = [
	{
		"constant": false,
		"inputs": [
			{
				"name": "candidate",
				"type": "string"
			}
		],
		"name": "addCandidate",
		"outputs": [],
		"payable": false,
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"constant": false,
		"inputs": [
			{
				"name": "candidate",
				"type": "string"
			}
		],
		"name": "vote",
		"outputs": [],
		"payable": false,
		"stateMutability": "nonpayable",
		"type": "function"
	},
	{
		"inputs": [],
		"payable": false,
		"stateMutability": "nonpayable",
		"type": "constructor"
	},
	{
		"constant": true,
		"inputs": [
			{
				"name": "index",
				"type": "uint8"
			}
		],
		"name": "getCandidate",
		"outputs": [
			{
				"name": "",
				"type": "string"
			}
		],
		"payable": false,
		"stateMutability": "view",
		"type": "function"
	},
	{
		"constant": true,
		"inputs": [],
		"name": "getNumOfCandidate",
		"outputs": [
			{
				"name": "",
				"type": "uint8"
			}
		],
		"payable": false,
		"stateMutability": "view",
		"type": "function"
	},
	{
		"constant": true,
		"inputs": [
			{
				"name": "candidate",
				"type": "string"
			}
		],
		"name": "getScore",
		"outputs": [
			{
				"name": "",
				"type": "uint256"
			}
		],
		"payable": false,
		"stateMutability": "view",
		"type": "function"
	}
]
```

3. `const contractAddress = '"0xd17504087ce962469fffb2b0ceef75ecc6a7487d"'`

4. `let voteContract = new web3.eth.Contract(abi, contractAddress)`



## 2. 두번째 실습

1. ganache 설치
   가상으로 이더리움 계좌를 생성해주고 연결할 수 있는 프로그램

![ganach](C:\Users\kooks\Desktop\Blog\kooks7.github.io\assets\img\ganach.png)

**설정**

* 트랜잭션이 발생하면 자동적으로 마이닝을 해서 실제와 같은 상황 구현

2. node 연결 파일

   ```javascript
   var Web3 = require('web3')
   var web3  = new Web3('http://localhost:8545')
   
   const abi = [
   	{
   		"constant": false,
   		"inputs": [
   			{
   				"name": "_value",
   				"type": "string"
   			}
   		],
   		"name": "setValue",
   		"outputs": [],
   		"payable": false,
   		"stateMutability": "nonpayable",
   		"type": "function"
   	},
   	{
   		"inputs": [
   			{
   				"name": "_value",
   				"type": "string"
   			}
   		],
   		"payable": false,
   		"stateMutability": "nonpayable",
   		"type": "constructor"
   	},
   	{
   		"constant": true,
   		"inputs": [],
   		"name": "getValue",
   		"outputs": [
   			{
   				"name": "",
   				"type": "string"
   			}
   		],
   		"payable": false,
   		"stateMutability": "view",
   		"type": "function"
   	}
   ]
    
   // 트랜잭션 주소
   const contractAddress = "0x4114e939fd2a2a74e1f8c387f5431674fad7e272"
   
   var helloContract = new web3.eth.Contract(abi, contractAddress)
   
   async function sendTest () {
   	let result = await helloContract.methods
   		.setValue("123")
   		.send({from : "0x9Ab00eD3d4A0E09a0350D4284436a5b298D6E945"}) //  수수료를 내는 계정
   	// console.log(result)
   }
   
   sendTest()
   
   async function hello() {
   	let result = await helloContract.methods.getValue().call()
   	console.log(result)
   }
   
   hello()
   ```

3. constructor 를 설정해주면 deploy를 할때 값을 입력해서 배포할 수 있다.

![remixConstructor](C:\Users\kooks\Desktop\Blog\kooks7.github.io\assets\img\remixConstructor.png)

4. node 파일을 실행해주면 value의 값이 바뀐것을 볼 수 있다.

## 3. 세번째 실습

​	**html 파일에 이더리움 연결하기**

1. contractTest.html 파일 생성

```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <meta http-equiv="X-UA-Compatible" content="ie=edge">
        <title>Document</title>
        <script type="text/javascript" src="https://cdn.jsdelivr.net/gh/ethereum/web3.js@1.0.0-beta.34/dist/web3.min.js"></script>
        <script>
            var web3  = new Web3('http://localhost:8545')

            const abi = [
                {
                    "constant": false,
                    "inputs": [
                        {
                            "name": "_value",
                            "type": "string"
                        }
                    ],
                    "name": "setValue",
                    "outputs": [],
                    "payable": false,
                    "stateMutability": "nonpayable",
                    "type": "function"
                },
                {
                    "inputs": [
                        {
                            "name": "_value",
                            "type": "string"
                        }
                    ],
                    "payable": false,
                    "stateMutability": "nonpayable",
                    "type": "constructor"
                },
                {
                    "constant": true,
                    "inputs": [],
                    "name": "getValue",
                    "outputs": [
                        {
                            "name": "",
                            "type": "string"
                        }
                    ],
                    "payable": false,
                    "stateMutability": "view",
                    "type": "function"
                }
            ]
            
            // 트랜잭션 주소
            const contractAddress = "0x4114e939fd2a2a74e1f8c387f5431674fad7e272"

            var helloContract = new web3.eth.Contract(abi, contractAddress)

            async function sendTest () {
                let result = await helloContract.methods
                    .setValue("123")
                    .send({from : "0x9Ab00eD3d4A0E09a0350D4284436a5b298D6E945"}) //  수수료를 내는 계정
                // console.log(result)
            }

            sendTest()

            async function hello() {
                let result = await helloContract.methods.getValue().call()
                console.log(result)
            }

            hello()
        </script>
    </head>
    <body>
        
    </body>
    </html>
          
```



2. contractTest.html  실행
3. console 확인하면 `setValue` 에 설정한 값 출력됨을 확인 할 수 있다.






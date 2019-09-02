---
layout: post
title:  "DailyStudy(스마트 컨트랙트)"
categories : DailyStudy!
date:   2019-09-02




---

### August..2019  (FRI)

### Learned Today 

## 솔리디티 프로그래밍



**솔리디티 언어**

* 이더리움 기반의 스마트 컨트랙트를 작성할 수 있는 객체지향형 프로그래밍 언어
* 스마트 컨트랙트는 이더리움 가상 머신인 EVM 에서 실행
* 솔리디티 소스 파일의 확장자는 .sol
* 솔리디티를 사용하면, 투표를 위한 DApp 부터, 크라우드 펀딩 서비스, 경매시스템, 다중 지갑 등의 서비스들을 구현할 수 있음
* 솔리디티를 이용하여 DApp(Decentralized application) 개발
* 솔리디티 컴파일러 - 솔크(Solc)
* 개발 환경 : remix ide

**Remix IDE**

* 바이트 코드
* ABI
* 블록체인에 배포

<remixIde.png 사진 넣기>

**코드 작성**

```javascript
pragma solidity ^0.4.11;

contract HelloWolrd { //contract 명
    string public greeting; 
    
    function HelloWorld(string _greeting) {
        geeting = _greeting;
    }
    
    function setGreeting(string _greeting) {
        greeting = _greeting;
    }
    
    function say() constant returns (string){
        return greeting;
    }
}
```

1. 컴파일러 버전 바꾸기
2. geth 실행시키기
3. Environment Web3 Provider로 바꾸기
4. geth 에서 트랜젝션 보낼 계정 풀기
5. 트랜젝션 보내기
6. 마이닝 하기

**Environment**

콘트랙트에 배포 블록체인에 기록해주세요가 deploy 이다. 빨간색의 버튼과 파란색의 버튼은 다르다. deploy를 누르면 배포해달라는것. 블록체인 노드에 컨트렉트가 간다. 실행할수있는 컨트랙트가 생김 함수도 동작한다. 파란색은 유저가 굳이 마이닝을 하지 않아도 실행이 된다.

### 솔디디티 언어

**컨트랙트**   
컨트랙트는 이더리움 어플리케이션의 기본적인 구성 요소로, 모든 변수와 함수는 어느 한 컨트랙트에 속한다. 

```
contract HelloWorld{
    
}
```

솔리디티 코드는 컨트랙트 안에 싸여 있다.

**Version Pragma**  
모든 솔리디티 코드는 "version pragma" 로 시작해야 하는데, 이는 해당 코드가 이용해야 하는 솔디디티 버전을 선언하는 것이다.

```
prgma solidity ^0.4.19;

contract HelloWorld{

}
```

**상태 변수**  
상태 변수는 컨트랙트 저장소에 영구적으로 저장된다. 즉, 이더리움 블록체인에 기록된다. 데이터베이스에 데이터를 쓰는 것과 동일하다.

``` java
contract Example {
    // 이 변수는 블록체인에 영구적으로 저장된다.
    unit myUnsignedInteger = 100;
}
```

이 컨트랙트에서는 myUnsignedInteger 라는 unit를 생성하여 100이라는 값을 저장했다.

**부호 없는 정수: unit**   
uint 자료형은 부호 없는 정수로, 값이 음수가 아니어야 한다. 부호 있는 정수는 int 를 사용한다.

**구조체**  
솔리디티는 구조체를 제공한다. 구조체를 통해 여러 특성을 가진 자료형을 생성할 수 있다.

```java	
struct Person{
    uint age;
    string name;
}
```



## ToDo

1. 추후 솔리디티 언어 문법 정리하기
2. ABI 정리하기




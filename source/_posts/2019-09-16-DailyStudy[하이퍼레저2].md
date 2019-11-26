---
layout: post
title:  "DailyStudy[하이퍼레저2]"
categories : DailyStudy!
date:   2019-09-16



---



## 하이퍼레저



### Hyperledger Fabric Component

1. Network
   * 블록 체인 네트워크를 구성하는 데이터 처리 Peer 들의 집합
   * 네트워크는 일관되게 복제 되는 Ledger를 유지 관리
2. Channels
   * 오직 이해관계자에게만 트랜잭션을 볼 수 있도록 하는 데이터 파티셔닝 메커니즘
   * 각 채널은 해당 특정 채널에 대한 트랙잭션만 포함하는 독립적인 트랜잭션 블록체인
3. Chaincode
   * 스마트계약, 자산 정의와 자산 수정을 위한 비지니스 로직 (or 트랜잭션)을 캡슐화 (프로그래밍)
   * 트랜잭션은 Chaincode를 실행함으로서 Ledger를 변경
4. Ledger
   * 네트워크의 현재 상태와 일련의 트랜잭션 호출이 포함
   * 공유되고 권한이 부여된 Ledger는 기록을 추가할 수 있는 시스템이며, 신뢰 할 수 있는 단일 소스로 제공
5. World State
   * 네트워크의 모든 자산에 대한 최신데이터를 반영
   * 데이터는 효율적인 엑세스를 위해 데이터베이스에 저장
   * LevelDB, CouchDB(Document Type) 지원
6. Ordering Service
   * 트랜잭션을 블록으로 정렬하는 모듈
7. Membership Service Provider(MSP)
   * 클라이언트 및 Peer들에게 ID 및 허가된 엑세스를 관리



### Certificate

* 사용자, Non-validating Peer, Validating Peer 등 모든 엔티티에 발행
* ECert(Enrollment Certificate)
  * 사용자의 신원을 확인하기 위해서 장기적으로 사용되는 인증서
  * 사용자, 검증노드 및 비검증 노드에 발행
* TCert(Transaction Certificate)
  * 트랜잭션마다 발행되는 단기적으로 사용되는 인증서
  * 사용자,검증 노드 및 비검증 노드에게 발행



## 트랜잭션(Transaction)

**Build Proposal** - user가 원장에 R/W하는 트랜잭션을 요청하고 dapp이 endorsing peer에게 전달해주는 단계

**Endorsement** - Endorsing peer들이 트랜잭션을 전달받고 다음 항목들을 검사한다. 

1. 트랜잭션 형식이 적절한지 여부
2. 이전에 동일한 트랜잭션 제출 여부 (replay-attack 방지) 
3.  MSP를 통한 서명 유효 여부
4. 요청에 대한 사용자의 권한 여부. 이상이 없으면 체인코드를 시뮬레이션한 후 그 결과값(read/write set)을 endorsing peer 자신의 서명과 함께 반환

**Ordering** - 위에서 반환된 결과값과 서명은 다시 orderer에게 전송되고 orderer는 이 트랜잭션들을 정렬한 후 블록을 생성하고 committing peer들에게 전송한다.

**Validate & Commit** - 블록을 전달받은 peer들은 블록에 포함된 트랜잭션들이 보증 정책을 준수하는지 여부와 read/write set 값이 적절한지 확인한다. 확인이 끝나면 트랜잭션 마다 valid/invalid 태그를 표시하여 자신의 원장에 저장하고, 유효한 트랜잭션의 write set을 world state에 포함시킨다.


  

## 실습 환경

- Docker 18.06.1-ce
- Ocker-compose: 1.21.2
- Golang : 1.10.3
- Node.js 8.10.0
- npm: 5.6.0

실습은 추후 업데이트 하겠다.
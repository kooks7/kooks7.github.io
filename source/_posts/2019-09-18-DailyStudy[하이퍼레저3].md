---
layout: post
title:  "DailyStudy[하이퍼레저3]"
categories : DailyStudy!
date:   2019-09-25




---



## 하이퍼레저

## SDK for Node.js

### 하이퍼레저 패브릭 SDK for Node.js 는 두개의 모듈로 구성

- fabric-client: 하이퍼레저 패브릭 클라이언트 용 API를 제공 -gRPC 프로토콜로 통신

**체인코드 호출 시 처리 흐름**

1. 초기화 처리  
   채널,조직/피어,오더러,MSP,EventHub 설정
2. 사용자 설정  
   MSP에 등록과 컨텍스트 설정
3. 체인코드 호출  
   조회/갱신 요청 발생 (수행 요청 및 커밋)
4. 이벤트 결과 수신 (옵션)

**체인 코드 호출의 두가지 유형**


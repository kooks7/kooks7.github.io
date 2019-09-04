---
layout: post
title:  "DailyStudy(Solidity2)"
categories : DailyStudy!
date:   2019-09-04



---



## Learned Today 

## Solidity

### 1. 투표 앱 만들기

```javascript
pragma solidity ^0.5.8;

contract Vote{

    uint8 numOfCandidate = 0;
    mapping(address => bool) isVoted; // 특정 유저가 투표 했는지 확인
    mapping(string => uint) score; // 각 후보자별 득표수
    mapping(uint8 => string) candidateList; // 후보자 리스트
    constructor() public{

    }

    // 후보자 생성
    function addCandidate (string memory candidate) public {
        candidateList[numOfCandidate] = candidate;
        numOfCandidate ++;
    }

    // 투표하기
    function vote (string memory candidate) public {
        score[candidate] ++;
    }

    // 후보자 수
    function getNumOfCandidate() public view returns (uint8) {
        return numOfCandidate;
    }

    // 특정 후보자 누구인지
    function getCandidate(uint8 index) public view returns (string memory ) {
        return candidateList[index];
    }

    // 특정 후보자가 얼마나 득표했는지
    function getScore(string memory candidate) public view returns (uint){
        return score[candidate];
    }


}
```

위 예시의 문제점

1. 중복투표 가능 => bool로 확인

2. 후보 추가 권한이 제한되어 있지 않음. => owner만 할 수 있게 바꾸기

수정코드 V.2

```javascript
pragma solidity ^0.5.8;

contract Vote{

    uint8 numOfCandidate = 0;
    mapping(address => bool) isVoted; // 특정 유저가 투표 했는지 확인
    mapping(string => uint) score; // 각 후보자별 득표수
    mapping(uint8 => string) candidateList; // 후보자 리스트
    address payable owner;

    constructor() public{
        owner = msg.sender;
    }

    modifier ownerOnly () {
        require(msg.sender==owner);
        _;
    }

    modifier checkDuplicate() {
        require(!isVoted[msg.sender]);
        _;
    }
    // 후보자 생성
    function addCandidate (string memory candidate) public ownerOnly {
        bool found = false;
        for(uint8 i=0; i<numOfCandidate; i++){
            if(keccak256(bytes(candidateList[i])) == keccak256(bytes(candidate))){ // 문자열 비														// 교가 안되기 때문에 keccak으로 비교
                found = true;
                break;
            }
        }
        require (!found);

        candidateList[numOfCandidate] = candidate;
        numOfCandidate ++;
    }

    // 투표하기
    function vote (string memory candidate) public checkDuplicate {
        score[candidate] ++;
        isVoted[msg.sender] = true;
    }

    // 후보자 수
    function getNumOfCandidate() public view returns (uint8) {
        return numOfCandidate;
    }

    // 특정 후보자 누구인지
    function getCandidate(uint8 index) public view returns (string memory ) {
        return candidateList[index];
    }

    // 특정 후보자가 얼마나 득표했는지
    function getScore(string memory candidate) public view returns (uint){
        return score[candidate];
    }


}
```






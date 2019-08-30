---
layout: post
title:  "DailyStudy"
categories : DailyStudy!
date:   2019-08-29



---



## August.29.2019  (THU)

## Learned Today 



## GitHub 프로젝트 관리 특강

저장소보다는 협업의 장소로 생각하자.  

### 1. GitHub 첫 시작 push / pull   

대장(첫 프로젝트 시작)

1. git init
2. git status 
3. README.md 와 코드 만들기
4. git add .                    // stage에 올림
5. git commit -m "first commit"         //  올라간 파일을 찍기 
6. git log                                          // commit 된 파일들을 hash 해서 버전 관리를 함
7.  git remote -v // 원격 저장소의 버전
8.  git remote add origin "<URL>"
9.  git push -u origin master

 부하  

1. git clone "<URL>"  // 프로젝트 가져오기
2. 코드 수정하기
3. git add / commit / push
4. git remote -v // 원격 저장소의 버전

대장

1. git pull origin master
2. 수정
3. git add / commit / push

### 2. fork-branch

다른 사람이 만든 코드를 들고오고 수정해서 제안한다.

대장

1. mkdir pullrequest
2. cd pullrequest
3. ///

부하

1. 대장 레포지터리 fork 하기
2. git clone https://github.com/kooks7/PullReq.git
3.  수정
4. git add README.md
5. git commit -m ""
6. git push origin master

대장

1. git pull origin master

## branching

1. index.html 만들기
2. git add .
3. git commit -m ""



### git checkout

1. git checkout <log> // log로 돌아감
2. git checkout master
3. git branch side
4. git checkout side
5. git commit

### branch 만들기

1. git branch side
2. git checkout side // side branch로 이동
3. 코드 수정
4. git checkout master

모든 프로젝트는 side branch에서 진행하고 merge 한다.





### commit 규칙  

1. 주어는 생략하고 동사(원형) + 목적어  // ex) "add skillset"



### branch 합치기

1. branch master로 가서 git merge side
2. git log --oneline --graph
3. git merge member
4. visual code 에서 수정 완료하기
5. git add index.html
6. git commit -m ""

### 원격저장소 별명

origin : 원격 저장소 이름

1. git remote add root





## Todo List


---
layout: post
title:  "[Git] 사용법4 - Cherry-pick & rebase"
categories : Coding!
tag :
- Git
date: 2020-07-09





---

Git 사용법 4 Cherry-pick 과 rebase를 알아봅시다.

<!-- more -->

# cherry-pick 과 rebase

# 1. cherry-pick 기본   

> cherry-pick은 특정 변화를 꼭 찝어서 가져오는 기능입니다.

1. 기본 설정

   ```bash
   
   1. 새로운 파일 만들기
   kooks@DESKTOP-81JHCMI MINGW64 ~/Desktop/cherry_pick (master)
   $ touch init.txt
   
   2. add
   $ git add init.txt
   
   3. init
   $ git commit -m 'init'
   [master (root-commit) 77ddab9] init
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 init.txt
   
   4. 로그 확인
   $ git log --oneline --all --graph
   * 77ddab9 (HEAD -> master) init 
   
   ```

2. 'init' commit 한 시점에서 새 브랜치 만들고 커밋 두개 올리기

   ```bash
   1. 토픽 브랜치 만들고 확인하기
   $ git log --oneline --all --graph
   * 77ddab9 (HEAD -> master, topic) init
   
   2. master에 커밋 추가
   $ touch m1; git add m1; git commit -m m1
   [master 0957a63] m1
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 m1
   
   3.	..
   $ touch m2; git add m2; git commit -m m2
   [master 00c1f8f] m2
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 m2
   
   4. 로그확인
   $ git log --oneline --all --graph
   * 00c1f8f (HEAD -> master) m2
   * 0957a63 m1
   * 77ddab9 (topic) init
   
   
   ```

3. topic 브랜치로 돌아가서, 커밋 세개 하기

   ```bash
   1. topic 브랜치로 돌아가기
   $ git checkout topic
   Switched to branch 'topic'
   
   2. 새 파일 만들기
   $ touch t1
   
   3. 커밋하기
   $ git add t1; git commit -m t1
   [topic 6bba7e4] t1
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 t1
   
   4. 새파일 만들고 커밋하기
   $ touch t2;add t2; git commit -m t2
   [topic d73e60f] t2
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 t2
   
   3. 세번째 커밋하기
   $ touch t3; git add t3; git commit -m t3
   [topic 4a6edde] t3
    1 file changed, 0 insertions(+), 0 deletions(-)
    create mode 100644 t3
   
   ```

#### cherry-pick 하기

현재 log를 보면 아래와 같습니다.

```bash
$ git log --oneline --all --graph
* 4a6edde (topic) t3
* d73e60f t2
* 6bba7e4 t1
| * 00c1f8f (HEAD -> master) m2
| * 0957a63 m1
|/
* 77ddab9 init

```

* master와 topic이란 브랜치 두개가 존재합니다.

* master에서 작업하다가 tolic의 t2 **commit이 생성될 때 변경된 부분만 가져오려면** 어떻게 해야할 까요?

  1. master 브랜치에 HEAD를 위치시킵니다.

  2. ```bash
     $ git cherry-pick d73e60
     ```

  3. 변경 된 디렉토리 확인하기

     ```bash
     $ ls
     init.txt  m1  m2  t2
     
     ```

     t2를 가져왔습니다.

  4. 로그를 보게 되면

     ```bash
     $ git log --oneline --all --graph
     * c642ff6 (HEAD -> master) t2
     * 00c1f8f m2
     * 0957a63 m1
     | * 4a6edde (topic) t3
     | * d73e60f t2
     | * 6bba7e4 t1
     |/
     * 77ddab9 init
     
     ```

     master 버전에 t2라는 commit이 생성되었습니다.

## 2. rebase 기본

> 한마디로 base를 바꾸는 기능입니다.

1. 기본 세팅

   ```bash
   $ git log --oneline --graph --all
   * ed52ae3 (HEAD -> topic) t3
   * 8c2bec3 t2
   * 7b2a9c2 t1
   | * 86d7881 (master) m2
   | * 39b0af6 m1
   |/
   * c825f47 init
   
   ```

   아까와 같은 상태로 topic, master branch를 만들어 줍니다.

2. 현재 master의 base는 분기가 시작된 init 입니다.

   topic의 base를 topic으로 변경하고 싶다면 어떻게 해야할까요?

   즉 init > t1 > t2 > t3 > m1 > m2 순으로 작업 순서를 변경하고 싶습니다.

#### rebase하기

1. 이동하고자 하는 브랜치인 master로 이동합시다.

   ```bash
   git checkout master
   ```

2. rebase 하기

   ```bash
   $ git rebase topic
   First, rewinding head to replay your work on top of it...
   Applying: m1
   Applying: m2
   
   ```

3. log 확인하기

   ```bash
   $ git log --oneline --graph --all
   * 1006f14 (HEAD -> master) m2
   * b7351ce m1
   * ed52ae3 (topic) t3
   * 8c2bec3 t2
   * 7b2a9c2 t1
   * c825f47 init
   
   
   ```

   

#### rebase vs merge

![merge_rebase](https://user-images.githubusercontent.com/47456161/87046117-b3918300-c233-11ea-8f42-ea269461890a.png)

## 단! rebase는 push 이후에 하면 안된다! 

### 결국 merge와 rebase의 최종 결과물은 같다.


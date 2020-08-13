---
layout: post
title:  "[Git] 사용법5 - Cherry-pick 과 rebase 충돌 원인 해결"
categories : Coding!
tag :
- Git
date: 2020-07-09






---

Git 사용법 Cherry-pick을 사용하면서 발생하는 충돌의 원인과 해결방법에 대해 알아봅시다..

<!-- more -->

## Cherry-pick 과 rebase 충돌 원인 해결

## 1. cherry-pick 에서 충돌

```
		  c	   c
		  m1   m1
		  	   m2
	c	. o -   o (master/HEAD)
o - o -
		` o  -  o  -  o (topic)
		  c	    c	 c
		  t1	t1	 t1
		  		t2   t2
		  			 t3
```

 master에서 topic의 두번째 commit을 cherry-pick 한다는 가정을 합시다.

1. master의 m2 

   ```
   c
   m1
   m2
   ```

   와 topic의 두번쨰 commit인

   `t2`

   는 충돌을 일으킵니다.

2. 이 부분은 3way merge를 사용해서 수동으로 해결해야 합니다. 

3. 결과

   ```
   		  c	   c	c
   		  m1   m1	m1
   		  	   m2	mt2
   	c	. o -   o -  o (master/HEAD)
   o - o -
   		` o  -  o  -  o (topic)
   		  c	    c	 c
   		  t1	t1	 t1
   		  		t2   t2
   		  			 t3
   ```

   

## 2. rebase에서 충돌

```
		   c	 c
		   m1    m1
		  	     m2
	c	. - o -   o (master/HEAD)
o - o -
		` o  -  o  -  o (topic)
		  c	    c	 c
		  t1	t1	 t1
		  		t2   t2
		  			 t3
```

master에서 topic의 변경 사항을 가져오게 됩니다.

1. master에서 `$ git rebase topic`을 실행합니다.
2. base
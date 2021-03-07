---
layout: post
title: 정규 표현식 cheat sheet
categories: basic
tag:
  - argument
date: 2021-03-07
image: assets/images/regex.png

---

자주 햇갈리는 정규 표현식. 알면 유용하게 사용할 수 있습니다.
정규 표현식에 대해 알아봅시다.

<!-- more -->

## 정규 표현식 cheat sheet

정규 표현식은 검색을 위해 개발된 방법입니다.

` /regex?/i` 형태로 되어 있습니다.

regex : 패턴

i : 플래그

## Groups and ranges

* `|` : 또는
* `()` : 그룹
* `[]` : 문자셋, 괄호안의 어떤 문자든
* `[^]`: 부정 문자셋, 괄호안의 어떤 문가 아닐때
* `(?:)` : 찾시만 기억하지는 않음

사용하기

1. `/(Hi|Hello)|(And)/` : Hi,Hello 는 그룹 1, And는 그룹2로 찾아집니다.
2. `/gr(e|a)y/` : gr로 시작하고 e나a가 중간에 들어가고, y로 끝난다.
3. `/gr[aed]y` : gr로 시작하고 중간에 a,e,d 가 들어가고 y로 끝난다.
4. `/gr[a-f]y` : gr로 시작하고, 중간에 a~f (알파벳 순서) 가 들어가고 y로 끝난다.
5. `[a-zA-Z0-9]` a 부터 z 까지, A 부터 Z 까지,   0 부터 9 까지 모든 문자열을 찾는다.
6. `[a-zA-Z0-9]` 5번을 제외한 모든 문자열을 찾는다. 즉, 특수문자들을 찾는다.
7. `/gra?y/` : gr와 y사이에  a가 있거나 없는 경우.
8. `/gra*y/` : gr사이에 a가 있거나, 없거나 여러개가 들어간 경우.
9. `/gra+y/` : gr사이에 a가 있거나, 여러개가 들어간 경우.
10. `/gra{2}y/` : gr사이에 a가 두개 있는 경우.
11. `/gra{2,}y/` : gr사이에 a가 최소 두개 있는 경우.
12. `/gra{2,4}y/` : gr사이에 a가 최소 두개, 최대 4개 있는 경우.

## Boundary-type

* `\b` : 단어 경계
* `\B` : 단어 경계가 아님
* `^` 단어의 시작
* `$` 단어의 끝

사용하기

1. `/\bYa/` : 단어 앞 경계에서 쓰이는 Ya를 찾는다.
2. `/Ya\b/` : 단어 뒤 경계에서 쓰이는 Ya를 찾는다.
3. `/Ya/B/` : 단어 경계가 아닌 곳에서 쓰이는 Ya를 찾는다.
4. `/^Ya/` : 단어 맨 처음에서 쓰이는 Ya를 찾는다.
5. `/Ya$/` : 단어 맨 마지막에서 쓰이는 Ya를 찾는다.

## Character classes

* `\` : 특수 문자가 아닌 문자
* `.`   : 어떤 글자 (줄마꿈 문자 제외)
* `\d` : digit 숫자
* `\D` : digit 숫자 아님
* `\w` : word 문자
* `\W` : word 문자아님
* `\s` : space 공백
* `\S` : space 공백 아님 

사용하기

1. `/\d/` : 숫자만 찾기
2. `/\w/` : 문자만 찾기

## 직접 사용하기

#### case 1. 전화번호

1. `/\d\d\d-\d\d\d\d-\d\d\d\d/` : 010-1234-5678
2. `/d{2,3}[- .]\d{3}[- .]\d{4}/`

#### case 2. 이메일

1. `/[a-zA-Z0-9._+-]+@[a-zA-Z0-9-]+.[a-zA-Z0-9.]+`

#### case 3. query 가져오기

1. `/(?:https?:\/\/)?(:?www\.)?youtu.be\/([a-zA-Z0-9-]{11}) /` : https or http가 있을 수 도 있고, 없을 수 도 있고

## JavaScript에서 사용하기

```javascript
const regex = /(?:https?:\/\/)?(:?www\.)?youtu.be\/([a-zA-Z0-9-]{11})/
const url = 'https://www.youtu.be/-ZClicWm0zM'
url.match(regex)

/**
[
  'https://www.youtu.be/-ZClicWm0zM',
  'www.',
  '-ZClicWm0zM',
  index: 0,
  input: 'https://www.youtu.be/-ZClicWm0zM',
  groups: undefined
] 
**/
```


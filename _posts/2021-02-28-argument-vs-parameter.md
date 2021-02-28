---
layout: post
title: "argument vs parameter"
categories: basic
tag:
  - argument
date: 2021-02-28
image:
---

argument vs parameter에 대해 알아봅시다.

<!-- more -->

## argument vs parameter

argument와 parameter를 혼동해서 사용하는 경우가 많습니다.

두 용어 차이에 대해 알아보도록 하겠습니다.

parameter는 함수 혹은 메서드 정의에 나열되는 변수 명입니다. 반면, argument는 함수나 메서드를 사용할 때 전달 해주는 실제 값입니다.

간단하게 설명하자면, prameter는 변수이고 argument는 실체입니다.


|               | 한글           | 의미                                  |
| ------------- | -------------- | ------------------------------------- |
| **parameter** | 매개변수       | 함수, 메서드 입력 변수(Variable) 이름 |
| **argument**  | 전달인자, 인자 | 함수, 메서드 입력 값(Value)           |



**Parameter(매개변수)**

```javascript
const parseDate = (req, res) = {
  return paramObject(req)
}
```

parseDate를 정의하고 있습니다. parseDate로 보내는 req와 res는 파라미터입니다.

**Argument(전달인자)**

```javascript
parseDate(req, res);
```

함수를 사용할 때, 입력값 req와 res는 argument 입니다.

##### 참고

- https://stackoverflow.com/questions/1788923/parameter-vs-argument
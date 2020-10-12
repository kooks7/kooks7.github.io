---
layout: post
title:  "[JavasSript] 객체에 대해서"
categories : Coding!
tag :
- JavasSript
date: 2020-08-25
image: assets/images/oop.png


---

객체지향을 많이 들어보긴 했지만 모르는 부분이 많습니다. JavaScript를 사용하는 객체지향에 대해 알아보도록 하겠습니다.

<!-- more -->

## JavaScript에서 사용하는 객체

우선 객체에 대한 설명은 넘어가도록 하겠습니다. 조금 이상하다고 느꼈던 부분 부터 시작하도록 하겠습니다.

#### this

> **this** 키워드는 지금 동작하고 있는 코드를 가지고 있는 객체를 가르킵니다.

```javascript
const person = {
	name: 'MJ'
  age: 27
  greeting: function() {
		alert(`Hi! My name is ${this.name}`)
  }
}
```

this를 사용하는 이유는 동적으로 객체를 상성하는 경우에 동적으로 값을 할당하기 위해서 입니다. 아래의 예를 봅시다.

```javascript
var person1 = {
  name: 'MJ',
  greeting: function() {
    alert('Hi! I\'m ' + this.name + '.');
  }
}

var person2 = {
  name: 'Kim',
  greeting: function() {
    alert('Hi! I\'m ' + this.name + '.');
  }
}
```

### 객체지향 프로그래밍

> 객체지향을 간단하게 설명하자면 프로그램 내에서 표현하고자 하는 실 시계의 일들을 객체를 사용해서 모델링 하고, 객체를 사용해서 처리하는 방법을 말합니다.

객체지향에서 중요한 개념 중 하나는, **추상화** 입니다. 추상화란 대상을 단순한 것으로 간소화 하는것을 말합니다.

#### 클래스와 인스턴스

> 클래스는 설계도라 생각하면 됩니다. 특정 개념을 정의하는 설계도입니다.
>
> 인스턴스는 클래스 생성자 함수를 이용해서 만듭니다.
>
> 예를 들어 사람이라는 개념이 있다면 개개인은 인스턴스라 할 수 있습니다.

#### 상속

특정한 클래스가 있을 때 이보다 더 많은 정보를 가진 클래스가 있을 수 있습니다. 이런 경우, 클래스를 상속받아 다른 클래스를 만들면 됩니다. 하나의 클래스를 상속해서 만든 클래스를 child 클래스라 하고 상위 클래스를 parent클래스라 합니다.
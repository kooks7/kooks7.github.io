---
layout: post
title:  "[TypeScript] 클래스 문법"
categories : Coding!
tag :
- TypeScript
date: 2020-06-29






---

클래스 문법에 대해 알아보도록 합시다.

<!-- more -->

## Next-Gen JavaScript Syntax 사용하기

#### 1. 화살표 함수

`const add = (a: number, b: number) => a + b;`

TypeScript에서도 화살표 함수를 작성할 수 있습니다.

```typescript
const add = (a: number, b: number) => a + b;

const printOutput: (a: string | number) => void = (output) =>
  console.log(output);

const button = document.querySelector('button');

if (button) {
  // button.addEventListener('click', () => {}); 인자가 없으면 화살표 함수를 넣어줘야 한다
  button.addEventListener('click', (event) => console.log(event));
}

printOutput(add(5, 2));

```



#### 2. 매개변수

- 매개변수에 default 값 넣기

  ```typescript
  const add = (a: number, b: number = 1) => a + b;
  ```

  `=`을 사용해서 매개변수에 default값을 설정 할 수 있습니다.

  ```typescript
  const add = (a: number = 1, b: number) => a + b;
  
  printOutput(add(5)); // 에러
  ```

  하지만 default 값을 앞에 설정해주고 인자를 하나만 설정해주면 에러가 발생합니다. 왜냐하면 b의 값을 안넣어 줬기 때문입니다. 따라서 처음 경우처럼 default value는 마지막에 작성해야 합니다.

#### 3. rest 파라미터

사용자에게 input을 받아서 함수를 사용해야 할 때가 있습니다. 이 경우는 몇개의 인자가 들어올지 모르기 때문에 rest 파라미터를 사용하면 됩니다.

- 정해지지 않은 갯수 인자로 받기

  ```typescript
  const add = (...numbers: number[]) => {
    let result = 0;
    return numbers.reduce((curResult, curValue) => {
      return curResult + curValue;
    }, 0);
  };
  
  const addedNumbers = add(5, 10, 2, 3.7);
  
  ```


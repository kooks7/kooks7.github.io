---
layout: post
title: "[TypeScript] TypeScript 기본 타입"
categories: Coding!
tag:
  - TypeScript
date: 2020-06-23
---

TypeScript 기본 타입들에 대해서 알아보도록 하겠습니다.

<!-- more -->

# TypeScript 기본

#### 핵심 Syntax & 기능

# 1. 핵심 Types

- **number**
  - 1, 5.3, -10
- **String**
  - 'Hi'
  - "Hi"
  - `Hi`
- **Boolean**
  - true
  - false

#### 프로젝트에서 보기1

간단한 프로젝트 폴더를 만들고 Types에 대해 알아봅시다. {}

**폴더 구조**

- index.html
- app.ts
- app.js

lite-server 패키지를 이용해서 서버를 실행하도록 하겠습니다.

1. `index.html`

   ```html
   <!DOCTYPE html>
   <html lang="en">
     <head>
       <meta charset="UTF-8" />
       <meta name="viewport" content="width=device-width, initial-scale=1.0" />
       <title>TypeScript</title>
       <script src="app.js"></script>
     </head>
     <body></body>
   </html>
   ```

2) `app.ts`

   ```javascript
   function add(n1, n2) {
     return n1 + n2;
   }

   const number1 = 5;
   const number2 = 2.8;

   const result = add(number1, number2);
   console.log(result);
   ```

   실행하면 예상한 대로 7.8이라는 값을 얻을 수 있습니다.

3) `app.ts` 에서 number1의 값을 String으로 바꿔봅시다.

   ```typescript
   function add(n1, n2) {
     return n1 + n2;
   }

   const number1 = "5";
   const number2 = 2.8;

   const result = add(number1, number2);
   console.log(result);
   ```

   이제는 예상할 수 있습니다. 당연히 52.8이라는 값을 얻을 수 있습니다.

4) 이러한 로직 에러를 잡기 위해 TypeScript의 기능을 사용할 수 있습니다.
   `app.ts`

   ```typescript
   function add(n1: number, n2: number) {
     return n1 + n2;
   }

   const number1 = "5";
   const number2 = 2.8;

   const result = add(number1, number2);
   console.log(result);
   ```

   이 파일에는 에러가 있습니다. 함수의 첫번째 인자 n1은 number이지만 result에서 string 값을 넣어주는 것을 볼 수 있습니다. 이는 컴파일할 때 아래와 같은 에러가 발생합니다.

   ```bash
   $ tsc app.ts
   app.ts:8:20 - error TS2345: Argument of type '"5"' is not assignable to parameter of type
   'number'.

   8 const result = add(number1, number2);
                        ~~~~~~~
   ```

Found 1 error.

````

미리 에러를 알려주기 때문에 개발 과정에서 오류를 잡을 수 있습니다.

#### TypeScript는 정적 언어

- JavaScript : Dynamic types -> runtime 체크
- TypeScript: Static types -> 개발하는 동안 체크

TypeScript의 장점은 정적 타입이기 때문에 개발하는 동안 잘못된 Type을 잡아낼 수 있습니다. JavaScript는 동적으로 변수를 할당하므로 실행하는 동안 잘못된 부분을 잡아낼 수 밖에 없습니다.

- 굳이 필요없는 코드

  ```typescript
  function add(n1: number, n2: number) {
    if (typeof n1 !== "number" || typeof n2 !== "number") {
      throw new Error("Incorrect input!");
    }
    return n1 + n2;
  }

  const number1 = "5";
  const number2 = 2.8;

  const result = add(number1, number2);
  console.log(result);
  ```

  위 코드를 보면 typeof를 사용하여 type을 체크 합니다. 굳이 사용하지 않아도 개발하는 동안 TypeScript가 오류를 잡아냄으로 굳이 작성하지 않아도 됩니다.

#### 참고

모든 type은 소문자로 시작합니다.

- ~~String~~ -> **string**
- ~~Number~~ -> **number**

#### 프로젝트 적용하기 2

1. `app.ts`에 다양한 input을 넣어줍니다.

```typescript
function add(n1: number, n2: number, showResult: boolean, phrase: string) {
  const result = n1 + n2;
  if (showResult) {
    console.log(phrase + result);
  } else {
    return n1 + n2;
  }
}

const number1 = 5;
const number2 = 2.8;
const printResult = true;
const resultPhrase = "Result is: ";

const result = add(number1, number2, printResult, resultPhrase);
````

2. 변수에도 미리 type을 지정해줄 수 있습니다.

   ```typescript
   let number1: number;
   number1 = 5;
   ```

   다른 type을 넣게 되면 에러가 발생합니다.

   ```typescript
   let number1: number;
   number1 = "5";
   ```

#### 핵심

- **const**

  상수를 바로 할당하게 되면 다시 변경할 일이 없습니다. 따라서 type을 지정해줄 필요가 없습니다.

  ~~`const number: number = 10`~~ -> `const number = 10`

- **let**

  변수는 추후에 다른 값을 할당 할 수 있기 때문에 type을 지정해줘야 합니다.

  `let number1: number;`

이렇게 변수에 type을 미리 설정해 에러를 방지하는 기능이 TypeScript의 핵심입니다.

# 2. Type2

## 1. object

- TypeScript에서 미리 지정되지 않은 객체에 접근하면 에러가 발생합니다.

  - `app.ts`

  ```typescript
  const person = {
    name: "MJ",
    age: 30,
  };
  console.log(person.nickname);
  ```

  에러

  ```bash
  $ tsc app.ts
  app.ts:5:20 - error TS2339: Property 'nickname' does not exist on type '{ name: string; age: number; }'.

  5 console.log(person.nickname);
                       ~~~~~~~~
  ```

Found 1 error.

````

- 따라서 미리 객체에 어떤 key-value가 있는지 아래와 같이 알려줘야 합니다.

```typescript
const person: {
  name: string;
  age: number;
} = {
  name: "MJ",
  age: 30,
};
console.log(person.name);
````

## 2. Array

배열을 정의하기 위해서는 `string[]`,`number[]`,`any[]`등과 같이 사용할 수 있지만 `any[]`는 잘 사용하지 않습니다. 이는 TypeScript가 주는 이점이 없기 때문입니다.

```typescript
let favoriteActivities: string[];
favoriteActivities = ["Sports", "Reading"];
```

`app.ts`

```typescript
const person = {
  name: "MJ",
  age: 30,
  hobbies: ["Soccer", "Reading"],
};

let favoriteActivities: string[];
favoriteActivities = ["Sports", "Reading"];

for (const hobby of person.hobbies) {
  // hobbies의 각 value의 type은 string이기 때문에 toUpperCase 사용 가능
  console.log(hobby.toUpperCase());
}
```

## 3. Tuple

배열과 비슷하지만 길이가 고장된 배열입니다.

- `app.ts`

  ```typescript
  const person: {
    name: string;
    age: number;
    hobbies: string[];
    role: [number, string];
  } = {
    name: "MJ",
    age: 30,
    hobbies: ["Soccer", "Reading"],
    role: [2, "author"],
  };

  person.role.push("admin");
  person.role[1] = 10;
  ```

- 컴파일

  ```bash
  $ tsc app.ts
  app.ts:14:1 - error TS2322: Type '10' is not assignable to type 'string'.

  14 person.role[1] = 10;
     ~~~~~~~~~~~~~~
  ```

Found 1 error.

````

tuple은 index에 들어갈 type을 미리 정해놓았기 때문에 1번 index에 숫자를 할당하지 못합니다.
하지만 push는 허용합니다. 대신 TypeScript는 잘못된 값이 다시 할당되는 것을 방지합니다.

## 4. Enum

TypeScript에만 있는 타입으로, 자동으로 상수 식별자를 열거합니다.

- `app.ts`

```typescript
const ADMIN = 0;
const READ_ONLY = 1;
const AUTHOR = 2;

const person = {
  name: "MJ",
  age: 30,
  hobbies: ["Soccer", "Reading"],
  role: ADMIN,
};

if (person.role === ADMIN) {
  console.log("is admin");
}
````

특정 조건을 관리하기 위해 위처럼 변수에 숫자를 할당할 수 있습니다.

```typescript
enum Role {
  ADMIN,
  READ_ONLY,
  AUTHOR,
}
```

```typescript
enum Role {
  ADMIN = 0,
  READ_ONLY = 1,
  AUTHOR = 2,
}
```

```typescript
enum Role {
  ADMIN = "ADMIN",
  READ_ONLY = "READ_ONLY",
  AUTHOR = "AUTHOR",
}

if (person.role === Role.ADMIN) {
  console.log(Role.ADMIN); // ADMIN
}
```

위처럼 enum을 사용하게 되면 리터럴의 타입과 값에 이름을 붙여 사용할 수 있습니다.

## 5. Any

말 그대로 어떠한 값도 저장할 수 있는 타입입니다. 모든 자료형을 넣을 수 있지만 이것은 단점이 됩니다. 바닐라 JavaScript를 사용할 때와 똑같습니다.

## 6. Union

두가지 이상의 타입을 한번에 설정할 수 있는 방법입니다.

- `app.ts`

  ```typescript
  function combine(input1: number | string, input2: number | string) {
    let result;
    if (typeof input1 === "number" && typeof input2 === "number") {
      result = input1 + input2;
    } else {
      result = input1.toString() + input2.toString();
    }
    return result;
  }

  const combinedAges = combine(30, 26);
  console.log(combinedAges);

  const combinedNames = combine("MJ", "KIM");
  console.log(combinedNames);
  ```

  위 코드에서 input1과 input2에 `|`를 사용해서 number와 string을 동시에 지정했습니다. 이후 typeof를 사용해서 type체크를 해주면 됩니다.

## 7. Literal

`const`와 같이 값을 바꿀수 없는 변수에 숫자나 문자열을 할당하면 TypeScript에서는 자동으로 타입을 할당합니다.

- `app.ts`

  ```typescript
  function combine(
    input1: number | string,
    input2: number | string,
    resultConversion: "as-number" | "as-text"
  ) {
    let result;
    if (
      (typeof input1 === "number" && typeof input2 === "number") ||
      resultConversion === "as-number"
    ) {
      result = +input1 + +input2;
    } else {
      result = input1.toString() + input2.toString();
    }
    return result;
  }

  const combinedAges = combine(30, 26, "as-number");
  console.log(combinedAges);

  const combinedStringAges = combine("30", "26", "as-number");
  console.log(combinedStringAges);

  const combinedNames = combine("MJ", "KIM", "as-text");
  console.log(combinedNames);
  ```

  `resultConversion`에 문자열을 미리 할당해 다른 값이 들어오지 못하게 미리 막고 있습니다. 이처럼 리터럴 타입을 이용하게 되면 다른 값이 오는 것을 방지할 수 있습니다.

## 8. Alias

사용자가 직접 새로운 type을 지정할 수 있는 기능입니다. 위 상황에서 union type으로 일일이 input의 타입을 지정했습니다. 하지만 Alias type을 사용하면 간단하게 코드를 작성할 수 있습니다.

- `app.ts`

  ```typescript
  type Combinable = number | string;
  type ConversionDescriptor = 'as-number' | 'as-text';

  function combine(
    input1: Combinable,
    input2: Combinable,
    resultConversion: ConversionDescriptor
  ) {

        ...

  ```

#### Type Aliases & Object Types

Alias는 객체도 타입으로 만들 수 있습니다

- 예를들어

  ```typescript
  type User = { name: string; age: number };
  const u1: User = { name: "MJ", age: 27 };
  ```

이런방식으로 작동할 수 있습니다.

## 9. return시 void

C 언어에서는 함수가 아무것도 return 하지 않으면 void라 합니다. TypeScript에서도 아무것도 Return 하지 않으면 void라는 type을 지정합니다.

- `app.ts`

  ```typescript
  // return type : number
  function add(n1: number, n2: number) {
    return n1 + n2;
  }

  // return type : void
  function printResult(num: number) {
    console.log("Result : " + num);
  }

  printResult(add(5, 12));
  ```

#### return undefined vs return void

TypeScript에서는 두개는 엄연히 다릅니다.

- return undefined

  아래 코드는 잘못된 코드입니다.

  ```typescript
  function printResult(num: number): undefined {
    console.log("Result : " + num);
  }
  ```

  올바른 코드

  ```typescript
  function printResult(num: number): undefined {
    console.log("Result : " + num);
    return;
  }
  ```

- return void

  ```typescript
  function printResult(num: number): void {
    console.log("Result : " + num);
  }
  ```

정말 특별한 경우가 아니라면 void를 사용하고, TypeScript가 return 값을 추론할 수 있기 때문에 return type을 명시하지 않아도 됩니다..

## 10. Function

변수에 Function 키워드를 사용하여 type을 지정할 수 있습니다.

- `app.ts`

  ```typescript
  function add(n1: number, n2: number) {
    return n1 + n2;
  }

  function printResult(num: number): undefined {
    console.log("Result : " + num);
    return;
  }

  printResult(add(5, 12));

  let combineValues: Function;

  combineValues = add;
  // combineValues = 5; error

  console.log(combineValues(8, 8));
  ```

위에서 보듯 변수에 함수를 지정할 수 있습니다. 하지만 잘못된 함수를 지정할 가능성이 있기 때문에 TypeScript에서는 return type도 미리 지정할 수 있습니다.

- 화살표 함수로 input과 return type 미리 지정하기

  ```typescript
  function add(n1: number, n2: number) {
    return n1 + n2;
  }

  function printResult(num: number): void {
    console.log("Result : " + num);
  }

  printResult(add(5, 12));

  let combineValues: (a: number, b: number) => number;

  combineValues = add;
  combineValues = printResult; // return type이 void이기 때문에 에러가 발생합니다.

  console.log(combineValues(8, 8));
  ```

  #### callback

  - `app.ts`

    ```typescript
    function addAndHandle(n1: number, n2: number, cb: (num: number) => void) {
      const result = n1 + n2;
      cb(result);
    }
    addAndHandle(10, 20, (result) => {
      console.log(result);
    });
    ```

    콜백 함수를 작성할 때 input값과 return 값을 위와 같이 작성합니다.

    콜백 함수를 사용할 때는 return type을 명시하지 않아도 됩니다. 이미 콜백함수를 정의할 때 return type을 명시 했기 때문입니다.

  #### return type의 느슨함

  TypeScript에서는 input 타입은 정확하게 요구하지만 return 타입은 다소 느슨합니다.

  ```typescript
  function addAndHandle(n1: number, n2: number, cb: (num: number) => void) {
    const result = n1 + n2;
    return cb(result);
  }

  console.log(
    addAndHandle(10, 20, (result) => {
      return result;
    })
  );
  ```

  위 예에서 콜백 함수의 return 타입은 void 입니다. 하지만 숫자를 return해도 숫자가 출력됩니다.

## 11. Unknown

user Input을 받아야 하는 경우는 type을 정하기 어려울 수 있습니다. 이럴때 unknown을 사용합니다. unknown은 any보다 제한적입니다. 아래의 예시를 봅시다.

- unknown 사용

  ```typescript
  let userInput: unknown;
  let userName: string;

  userInput = 5;
  userInput = "Max";
  userName = userInput; // 에러 발생
  ```

- any 사용

  ```typescript
  let userInput: any;
  let userName: string;

  userInput = 5;
  userInput = "Max";
  userName = userInput; // 문제 없음
  ```

이 처럼 미리 타입이 정의된 다른 변수에 unknown을 할당하면 에러가 발생합니다.

이런 경우는 `typeof`를 사용하면 TypeScript가 타입 체크를 인지하고 에러를 막습니다.

- typeof 사용

  ```typescript
  let userInput: unknown;
  let userName: string;

  userInput = 5;
  userInput = "Max";
  // 문제 없음
  if (typeof userInput === "string") {
    userName = userInput;
  }
  ```

## 12. never

never은 함수가 return 할 수 있는 또 다른 타입입니다. throw 구문을 사용할 때 return type은 never입니다.

- never

  ```typescript
  function generateError(message: string, code: number): never {
    throw { message: message, errorCode: code };
  }

  generateError("An error occurred!", 500);
  ```

이 함수는 return 값이 있는것이 아니라 아무값도 return하지 않습니다.

- throw 함수를 return으로 받으려고 할때

  ```typescript
  function generateError(message: string, code: number) {
    throw { message: message, errorCode: code };
  }

  const result = generateError("An error occurred!", 500);
  console.log("result", result);
  ```

위 코드는 result에서 log가 찍히는 것이 아니라 throw 구문 자체에서 에러가 발생하는 로직입니다.

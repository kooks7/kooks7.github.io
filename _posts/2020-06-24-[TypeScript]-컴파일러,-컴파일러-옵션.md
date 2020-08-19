---
layout: post
title:  "[TypeScript] 컴파일러, 컴파일러 옵션"
categories : Coding!
tag :
- TypeScript
date: 2020-06-24





---

TypeScript 를 JavaScript로 바꾸는 컴파일러와 그 옵션들에 대해 알아보도록 하겠습니다.

<!-- more -->

# TypeScript 컴파일러

`tsc app.ts`같이 `tsc` 명령어를 사용해서 컴파일을 하게 되면 큰 프로젝트에서 생산성은 떨어질 것입니다. 큰 프로젝트에서는 어떻게 컴파일 하는지 알아보도록 하겠습니다.

## 1. Watch command 사용하기

- 기존에는 `tsc app.ts` 커맨드를 사용해서 수동적으로 컴파일 했습니다.
- `tsc app.ts --watch`나 `tsc app.ts -w` 커맨드를 사용하면 코드에 변경이 있을때 자동으로 컴파일 해줍니다.
- 코드에 오류가 있으면 자동적으로 오류를 알려주기도 합니다.

하지만 하나의 파일만 변경하고 있기 때문에 여전히 큰 프로젝트에서 여려 파일을 수정할 때 사용하기는 불편합니다.

#### 전체 파일 자동으로 컴파일 하기

1. `tsc --init` : tsconfig.json 파일이 생성됩니다.
2. `tsc -w`: 자동으로 폴대 내의 모든 파일을 컴파일 합니다.

## 2. tsconfig 파일

tsconfig 파일은 TypeScript가 어떻게 프로젝트 폴더를 컴파일하고 관리해야하는지 정의하는 파일입니다.

#### 옵션

1. **exclude**

   `"exclude": ["analytics.ts"]`

   컴파일 할 때 특정 파일을 제외하는 옵션입니다.

2. **include**

   `"include": ["app.ts"]`

   include 키워드를 사용하면 해당 리스트만 컴파일 하고 지정하지 않은 파일은 컴파일 하지 않습니다.

#### compilerOptions

tsconfig.json 파일을 보면 컴파일러 옵션이 있습니다. 하나씩 알아봅시다.

1. **target**

   어떤 JavaScript 버전으로 컴파일할 것인지 정의하는 옵션입니다. 기본적으로 es5가 지정되어 있습니다.

   - **es5** app.js

     ```javascript
     "use strict";
     var age;
     age = 30;
     var userName = 'MJ';
     console.log(userName);
     
     ```

   - **es6** app.js

     ```javascript
     "use strict";
     let age;
     age = 30;
     const userName = 'MJ';
     console.log(userName);
     
     ```

2. **lib**

   lib는 컴파일에 포함될 라이브러리 목록입니다. 

   - lib

     ```json
         "lib": [
           "DOM",
           "es6",
           "DOM.Iterable",
           "ScriptHost"
         ] 
     ```

   기본적으로 target을 설정하면 필요한 라이브러리가 포함되어 있습니다.

3. **sourceMap**

   sourceMap은 디버깅 및 개발에 사용합니다. 이 설정을 적용하면 브라우저의 Sources 탭에서 TypeScript 파일도 같이 확인할 수 있습니다.

4. **outDir, rootDir**

   각각 순서대로 파일이 저장되는 위치와 컴파일할 파일의 위치를 설정할 수 있습니다.

5. **noEmitOnError**

   기본적으로 TypeScript 파일에 에러가 있어도 JavaScript 파일로 컴파일 합니다. 에러가 있을때 컴파일 하지 않기 위해서 noEmitOnError 옵션을 true로 설정해주면 TypeSciprt파일에 에러가 있을때는 에러체크만 하고 JavaScript파일을 만들지 않습니다.

6. **strict**

   - **noImplicitAny**

     함수의 인자 타입을 엄격하게 제한하는 옵션

   - **strictNullChecks**

     null이나 undefined가 될 수 있는 값에는 느낌표나 그 변수를 체크해줘야 합니다.

     - 느낌표 사용

       ```typescript
       const button = document.querySelector('button')!;
       
       button.addEventListener('click', () => {
         console.log('Clicked!');
       });
       ```

     - if 체크

       ```typescript
       const button = document.querySelector('button')!;
       
       if (button) {
         button.addEventListener('click', () => {
           console.log('Clicked!');
         });
       }
       ```

7. **코드 품질 옵션**

   - **noUnusedLocals**

     사용하지 않은 로컬 변수가 있으면 알려줍니다.

   - **noUnusedParameters**

     함수에서 사용하지 않는 파라미터를 알려줍니다.

## 3. Visual Code를 사용한 Debug

1. ESLint pakage를 사용합니다.
2. Prettier
3. Debugger for Chrome

#### Debugger for Chrome

이 패키지를 사용하면 Chrome에서 애플리케이션을 사용하면서 디버거를 작동할 수 있습니다. 즉, 실제 runtime 환경을 가정하고 디버깅 할 수 있게 됩니다.

기존 파일을 난독화해서 브라우저가 이해하기 쉽게 만들어 성능을 향상 시킵니다. 이 난독화 된 파일은 디버깅이 어렵기 때문에 옵션을 true로 설정하게 되면 sourceMap을 생성하게 되고 난독화한 파일과 비교해가며 디버깅 할 수 있습니다.

#### 공식 DOCS

https://typescript-kr.github.io/pages/compiler-options.html




---
layout: post
title: Typescript 개요(1)
image: typescript_logo.png
categories: typescript
category: typescript
excerpt: typescript 공부한 내용들을 정리해보았습니다.
tags: [타입스트립트, typescript, vscode]
---

### Typescirpt 개요

✔️ [타입스크립트 핸드북 사이트](https://www.typescriptlang.org/ko/docs/handbook/intro.html)

- 타입스크립트는 자바스크립트에 타입이 입혀진 언어이다.
- 자바스크립트와 다르게 브라우저에서 실행하기 위해 파일을 한 번 변환(컴파일)해줘야 한다.  
<br />

---

### 타입 스크립트 설치
typescript는 2가지의 설치 방법이 있는 것 같다.  
- 1. **npm**을 통해 설치
- 2. **Visual Studio**에서 패키지 설치

1번 방식은 꼭 node가 설치되어 있어야만 사용가능하다.
2번 방식은 ASP.NET Core APP을 만들 때 사용하는 것 같다.  

![Untitled (6)](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/a13bee1b-7e13-4da7-9ac0-1ab78bf44d02)

나는 Node가 설치되어 있으므로 1번 방식으로 설치했다.  

{% highlight js %}

// 프로젝트 별 설치
npm install typescript --save-dev

// 글로벌 설치
npm install -g typescript

{% endhighlight %}

<br />

---

### TSC

- 타입스크립트 파일을 자바스크립트 파일로 변환(컴파일)해주는 명령어다.
- index.ts가 존재하는 폴더에서 아래 명령어를 실행하면 컴파일이 진행되고 별도의 js 파일이 생성된다.
- 참고로 tsc는 TypeScript Compiler의 약자이다.
- 프로젝트별 typescript를 설치하는 경우 **npx tsc**로 사용해야 한다.


{% highlight js %}

- 글로벌 typescript를 설치하면 자동적으로 tsc가 설치된다. 
tsc index.ts

// 프로젝트 별로 설치했다면 npx를 사용하면 된다.
npx tsc index.ts

{% endhighlight %}
<br />

--- 

### 타입스크립트를 써야 하는 이유

#### 1. 에러를 사전에 잡을 수 있음(정적 타입 검사)

- 프로그램을 실행시키지 않으면서 코드의 오류를 검출하는 것을 **정적 검사**라고 한다.
- TypeScript는 프로그램을 실행시키기 전에 값의 종류를 기반으로 프로그램의 오류를 찾는다.

{% highlight js %}
// @errors: 2551
const obj = { width: 10, height: 15 };
const area = obj.width * obj.heigth;

// obj안에 heigth는 없으므로 undefined
// 10 * undefined는 곱할 수 없는 값이므로 JS에서는 NaN을 반환하지만
// TS 에서는 오류로 간주한다.
{% endhighlight %}  

![Untitled (1)](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/42fec001-e100-44a0-b9ec-d2b2be7c5cad)

add 함수의 첫번째 매개변수 a는 숫자값이 와야 한다.  
10 + 10 = 20 이지만 10 + ‘10’ = 1010이 된다.  
숫자와 문자열을 더할 경우 숫자를 문자열로 인식하기 때문에 원하는 결과를 얻지 못한다.  
숫자가 아닌 문자열을 넣을 경우 VScode에서 빨간줄로 에러를 표시해주기 때문에 에러를 사전에 잡을 수 있다.

<br/>

#### 2. 코드 자동 완성과 가이드

JS와 다르게 TS는 타입이 정해져 있기 때문에 해당 타입에서 쓸 수 있는 API를 미리 보여줄 수 있다.  
사용하고 싶은 API는 **tab**키를 입력하면 글자를 자동 완성시켜 준다.  
(나도 모르게 **Enter** 쳐서 자동완성은 안되고 줄바꿈만 일어난 적이 빈번했다.ㅎㅎ)

![Untitled (2)](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/6dc06cd1-3037-4b2f-8a31-c993e6ed0de8)  

(이미지)


<br />

---

### JSDOC

- DOC 어노테이션을 추가하여 js를 typescript처럼 사용할 수 있다
- 한 번에 타입스크립트로 적용하는 것이 부담스러울 때 자바스크립트 코드에 JSDOC을 사용해 점차 typescript를 적용해 나갈 수 있다.  

![Untitled (5)](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/6142ed46-a912-4e4a-acb1-bddc42b5a90d)

- JS 파일이지만 JSDOC을 사용했기 때문에 typescript처럼 API 미리보기를 제공받을 수 있다.  

![Untitled (4)](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/1b7df9f7-2514-4c0c-8325-da1a5adebf74)  

- 또한 함수 이름 위에 마우스를 올리면 TS파일처럼 함수에 대한 타입 정보를 제공해준다.  

![Untitled (3)](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/7364a273-f2fd-4f9d-94f4-8bad5102fe7e)  

- @ts-check 를 추가하면 타입스크립트를 적용한 효과를 나타낼 수 있다.
- 어노테이션에 의해 타입을 체크하고 두번째 인자가 숫자여야 하는데 문자로 받았으므로 오류를 발생시킨다.
<br />

---

### tsconfig.json

✔️ [tsconfig reference 참고 사이트](https://www.typescriptlang.org/tsconfig)
- **tsconfig.json**은 TypeScript 프로젝트의 설정 파일이다.
- 프로젝트를 컴파일하는 데 필요한 루트 파일과 컴파일러 옵션을 지정할 수 있다.

{% highlight js %}
{
  "compilerOptions": {
    "allowJs": true, // 이 프로젝트 내 자바스크립트 사용 허용
    "checkJs": true, // @ts-check의 역할을 해줌(allowJs와 같이 사용)
    "noImplicitAny": true, // 모든 변수에 타입에 대해 any라도 넣어줘야 함
    "target": "es5", // 컴파일된 JavaScript의 대상 버전을 지정
    "module": "commonjs",
    "outDir": "dist", // 컴파일된 JavaScript 파일의 출력 디렉토리를 설정
    "strict": true // 엄격한 타입 체크를 활성화
  },
  "include": [
    "src/**/*.ts" // 컴파일 대상으로 포함할 TypeScript 소스 파일의 경로를 설정(src 디렉토리 아래의 모든 .ts 파일을 포함하도록 설정)
  ],
  "exclude": [
    "node_modules" // 컴파일 대상에서 제외할 파일이나 디렉토리의 경로를 설정(node_modules 디렉토리를 제외하도록 설정)
  ]
}
{% endhighlight %} 
<br />

---

### Playground

✔️ [Playground 사이트](https://www.typescriptlang.org/play)

- TypeScript 코드를 작성하고 실행하며 결과를 확인할 수 있는 온라인 도구이다.
- 타입스크립트를 설치하지 않아도 사용할 수 있는 장점이 있다.
- 또한 작성한 typescript가 어떻게 javascript로 변환되는 지 알 수 있다.  

- 왼쪽 편집기에 ts 코드를 작성하면 자동으로 js 코드로 변환해 오른쪽에 보여준다.
![Untitled (7)](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/63bcb25f-603a-4a20-8bce-009609c1a804)  

- **a**의 타입이 숫자인데 문자를 넣었기 떄문에 에러가 발생하는 것을 확인할 수 있다.
![Untitled (8)](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/2fa03c85-fe57-47f1-8a70-11bb0efccf6f)  
<br />


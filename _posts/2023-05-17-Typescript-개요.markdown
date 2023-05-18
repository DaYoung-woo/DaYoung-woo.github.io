---
layout: post
title: Typescript-개요
image: typescript.png
categories: typescript
excerpt: typescript를 공부하면서 배운 내용들을 정리해보았습니다.
tags: [타입스트립트, typescript, vscode]
---

### Typescirpt 개요

✔️ [타입스크립트 핸드북 사이트](https://www.typescriptlang.org/ko/docs/handbook/intro.html)

- 타입스크립트는 자바스크립트에 타입이 입혀진 언어이다.
- 자바스크립트와 다르게 브라우저에서 실행하기 위해 파일을 한 번 변환(컴파일)해줘야 한다.
  <br />

---

### 타입스크립트를 써야 하는 이유

#### 1. 에러를 사전에 잡을 수 있음(정적 타입 검사)

- 프로그램을 실행시키지 않으면서 코드의 오류를 검출하는 것을 **정적 검사**라고 한다.
- TypeScript는 프로그램을 실행시키기 전에 값의 종류를 기반으로 프로그램의 오류를 찾는다.

{% highlight js %}
// @errors: 2551
const obj = { width: 10, height: 15 };
const area = obj.width \* obj.heigth;

// obj안에 heigth는 없으므로 undefined
// 10 \* undefined는 곱할 수 없는 값이므로 JS에서는 NaN을 반환하지만
// TS 에서는 오류로 간주한다.
{% endhighlight %}
<br/>

add 함수의 첫번째 매개변수 a는 숫자값이 와야 한다.  
10 + 10 = 20 이지만 10 + ‘10’ = 1010이 된다.  
숫자와 문자열을 더할 경우 숫자를 문자열로 인식하기 때문에 원하는 결과를 얻지 못한다.  
숫자가 아닌 문자열을 넣을 경우 VScode에서 빨간줄로 에러를 표시해주기 때문에 에러를 사전에 잡을 수 있다.

<br/>

#### 2. 코드 자동 완성과 가이드

JS와 다르게 TS는 타입이 정해져 있기 때문에 해당 타입에서 쓸 수 있는 API를 미리 보여주고 사용하고 싶은 API를 tab을 이용해 글자를 자동 완성시켜 준다.
<br />

---

### JSDOC

- DOC 어노테이션을 추가하여 js를 typescript처럼 사용할 수 있다
- 한 번에 타입스크립트로 적용하는 것이 부담스러울 때 자바스크립트 코드에 JSDOC을 사용해 점차 typescript를 적용해 나갈 수 있다.

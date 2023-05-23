---
layout: post
title: Typescript의 everyday type(2)
image: typescript_logo.png
excerpt: 
  typescript의 기본 타입
categories: 리액트
tags: [타입스트립트, typescript, 타입]
---

✔️ [타입스크립트 핸드북 사이트](https://www.typescriptlang.org/ko/docs/handbook/2/everyday-types.html)  

<br />

### typescript의 원시 타입
- boolean
- number
- string

String, Number, Boolean와 같은 (대문자로 시작하는) 타입은 유효한 타입이지만, 코드상에서 이러한 특수 내장 타입을 사용하는 경우는 극히 드물다.  
항상 string, number, boolean 타입을 사용을 권장한다고 한다.

---

### boolean

- boolean 값이라고 일컫는 참/거짓(true/false) 값이다.

{% highlight ts %}
let show: boolean = true;
{% endhighlight %}
<br/>

---

### number

- 부동 소수에는 `number`라는 타입이 붙혀진다.  
- 16진수, 10진수 뿐만 아니라 진수, 8진수 리터럴도 지원한다.

{% highlight ts %}
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
{% endhighlight %}
<br/>

---

### string

- 텍스트 데이터 타입을 `string`으로 표현한다.  
- 큰따옴표 (`"`)나 작은따옴표 (`'`)를 문자열 데이터를 감싸는데 사용한다.  
- **템플릿 문자열**을 사용하면 여러 줄에 걸쳐 문자열을 작성할 수 있으며, 표현식을 포함시킬 수도 있다.

{% highlight ts %}
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
{% endhighlight %}
<br/>

---

### 배열

- 배열 타입은 두 가지 방법으로 쓸 수 있다.

#### 1. 배열 요소들을 나타내는 타입 뒤에 [ ] 를 사용
{% highlight ts %}
let list: number[] = [1, 2, 3];
{% endhighlight %}
<br/>


#### 2. 제네릭 배열 타입을 사용

- **Array<>** 꺽새 괄호 안에 사용할 타입을 입력해줘야 한다.
- **[number]**는 전혀 다른 의미를 가진다.(튜플 타입에서 참조)

{% highlight ts %}
// string, number와 다르게 Array는 첫 스펠링이 대문자
let arr: Array<number> = [1,2,3];
{% endhighlight %}  

- 만약 꺽새 괄호 안 타입과 다른 타입을 입력하면 오류로 표시된다.
{% highlight ts %}
// 'number' 형식은 'string' 형식에 할당할 수 없습니다.
let heroes: Array<string>= ['capt', 'Thor', 10]
{% endhighlight %}
<br/>

---

### any

- 특정 값으로 인하여 타입 검사 오류가 발생하는 것을 원하지 않을 때 사용할 수 있다.
- 사용자로부터 받은 데이터나 서드 파티 라이브러리 같은 동적인 컨텐츠에서 오는 값은 타입을 알지 못할 수도 있다.
- 이 경우 any를 사용하면 타입 검사를 하지 않고, 그 값들이 컴파일 시간에 검사를 통과시켜준다.
- object를 사용하면 되지 않을까? 생각할 수 있지만 object를 쓰면 오류가 발생할 수 있다.
{% highlight ts %}
let notSure: any = 4;
notSure.ifItExists(); // 성공, ifItExists 는 런타임엔 존재할 것입니다.
notSure.toFixed(); // 성공, toFixed는 존재합니다. (하지만 컴파일러는 검사하지 않음)

let prettySure: Object = 4;
prettySure.toFixed(); // 오류: 프로퍼티 'toFixed'는 'Object'에 존재하지 않습니다.
{% endhighlight %}

- any의 사용은 지양되고 있다.
- 컴파일러 플래그 **noImplicitAny**를 사용하면 암묵적으로 any로 간주하는 모든 경우에 오류를 발생시킬 수 있다.  
<br/>

---

### 함수

- 함수는 JavaScript에서 데이터를 주고 받는 주요 수단이다.
- TypeScript에서는 함수의 입력 및 출력 타입을 지정할 수 있다.

{% highlight ts %}
// 함수의 파라미터에 타입을 정의하는 방식
function sum(a: number, b: number) {
  return a + b;
}

sum(10, 20);

// 함수의 반환 값에 타입을 정의하는 방식
function sum(): number {
	return 10;
}

// 함수에 타입을 정의하는 방식
function add(a: number, b: number): number {
	return a + b;
}
{% endhighlight %}
<br />

- JS에서는 매개변수의 수와 인수가 일치하지 않아도 된다.  
![1](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/94c0b2bb-9a7e-4184-b1eb-b7d350e59718)
<br />

- 하지만 TS에서는 오류로 인식된다.  
![2](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/f35ddc45-9941-45ac-bf17-bbfd3f8fde59)  
![3](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/e5768c32-67d0-4de9-baa8-0a959ae5ff70)
<br />

- 또한 매개변수에 타입이 표기되었다면, 해당 함수에 대한 인자는 검사가 이루어진다.
{% highlight ts %}
// 매개변수 타입 표기
function greet(name: string) {
  console.log("Hello, " + name.toUpperCase() + "!!");
}

// 만약 실행되면 런타임 오류가 발생하게 됩니다!
greet(42);
Argument of type 'number' is not assignable to parameter of type 'string'.

{% endhighlight %}
<br />

### 익명함수

- 익명 함수는 코드상에서 위치한 곳을 보고 해당 함수가 어떻게 호출될지 알아낼 수 있다면, TypeScript는 해당 함수의 매개 변수에 자동으로 타입을 부여한다.

{% highlight ts %}
// 아래 코드에는 타입 표기가 전혀 없지만, TypeScript는 버그를 감지할 수 있습니다.
const names = ["Alice", "Bob", "Eve"];
 
// 함수에 대한 문맥적 타입 부여
names.forEach(function (s) {
  console.log(s.toUppercase());
Property 'toUppercase' does not exist on type 'string'. Did you mean 'toUpperCase'?
});
 
// 화살표 함수에도 문맥적 타입 부여는 적용됩니다
names.forEach((s) => {
  console.log(s.toUppercase());
Property 'toUppercase' does not exist on type 'string'. Did you mean 'toUpperCase'?
});
{% endhighlight %}
<br />

---
layout: post
title: Typescript의 everyday type(4)
image: typescript_logo.png
excerpt: 
  typescript의 기본 타입
categories: typescript
category: typescript
tags: [타입스트립트, typescript, 타입]
---
✔️ [타입스크립트 핸드북 사이트](https://www.typescriptlang.org/ko/docs/handbook/2/everyday-types.html#%EB%A6%AC%ED%84%B0%EB%9F%B4-%ED%83%80%EC%9E%85)

### 리터럴 타입

리터럴 타입은 특정 값을 나타내는 타입이다.  
리터럴 타입은 해당 값의 정확한 값과 타입을 정의할 수 있어 정확성과 제한성을 갖는다.

아래 코드처럼 정해진 문자열 값 이외의 값을 할당하면 에러가 발생한다.
{% highlight ts %}
let x: "hello" = "hello";
x = "hello"; 
x = "howdy"; // Type '"howdy"' is not assignable to type '"hello"'.
{% endhighlight %}  

위의 코드처럼 단 하나의 값만 가질 수 있는 코드는 잘 사용하지 않는다.  
하지만 리터럴을 유니언과 함께 사용하면, 특정 종류의 값들만을 인자로 받을 수 있는 함수를 정의하는 경우에 유용한 개념들을 표현할 수 있다.  

{% highlight ts %}
function printText(s: string, alignment: "left" | "right" | "center") {
  // ...
}
printText("Hello, world", "left");
printText("G'day, mate", "centre"); // Argument of type '"centre"' is not assignable to parameter of type '"left" | "right" | "center"'.
{% endhighlight %}  
<br />

숫자 리터럴도  같은 방식으로 사용할 수 있다.
{% highlight ts %}
function compare(a: string, b: string): -1 | 0 | 1 {
  return a === b ? 0 : a > b ? 1 : -1;
}
{% endhighlight %}  
<br />

물론, 리터럴이 아닌 타입과도 함께 사용할 수 있다.
{% highlight ts %}
interface Options {
  width: number;
}
function configure(x: Options | "auto") {
  // ...
}
configure({ width: 100 });
configure("auto");
configure("automatic"); // Argument of type '"automatic"' is not assignable to parameter of type 'Options | "auto"'.
{% endhighlight %}  
<br />

#### 리터럴 추론

객체를 사용하여 변수를 초기화하면, TypeScript는 해당 객체의 프로퍼티는 이후에 그 값이 변화할 수 있다고 가정한다.  
아래 코드를 보면, 기존에 값이 0이었던 필드에 1을 대입하였을 때 TypeScript는 이를 오류로 간주하지 않는다.
{% highlight ts %}
const obj = { counter: 0 };
obj.counter = 1;
obj.counter = '0'; // Type 'string' is not assignable to type 'number'.
{% endhighlight %}  
하지만 '0' 리터럴 타입은 오류로 간주한다.  
obj의 counter 프로퍼티는 이미 number 타입으로 추론되었기 때문에 리터럴 타입을 할당하면 오류가 발생한다.
<br />

--- 

### strictNullChecks  

null과 undefined는 모든 타입의 변수에 대입될 수 있다.  
Null 검사의 부재는 버그의 주요 원인이 된다.  
별다른 이유가 없다면, 코드 전반에 걸쳐 strictNullChecks 옵션을 설정하는 것을 항상 권장한다.
{% highlight ts %}
function testStrictNullChecks(x: string) {
  console.log(x)
}

testStrictNullChecks(undefined) // strictNullChecks를 사용하면 에러가 발생한다: Argument of type 'undefined' is not assignable to parameter of type 'string'.

// undefined도 허용하고 싶다면 유니언으로 선언해야 한다.
function doSomething(x: string | undefined) {
  if (x === undefined) {
    // 아무 것도 하지 않는다
  } else {
    console.log("Hello, " + x.toUpperCase());
  }
}
{% endhighlight %} 
<br />

#### Null 아님 단언 연산자 (접미사!)

명시적인 검사를 하지 않고도 타입에서 null과 undefined를 제거할 수 있는 특별한 구문이다.  
. 표현식 뒤에 !를 작성하면 해당 값이 null 또는 undefined가 아니라고 타입을 단언할 수 있다.
 이 구문은 코드의 런타임 동작을 변화시키지 않으므로, ! 연산자는 반드시 해당 값이 null 또는 undefined가 아닌 경우에만 사용해야 한다.
{% highlight ts %}
function liveDangerously(x?: number | undefined) {
  // 오류 없음
  console.log(x!.toFixed());
}
{% endhighlight %} 
<br />

---

### 열거형
✔️ [타입스크립트 핸드북 사이트](https://www.typescriptlang.org/ko/docs/handbook/enums.html)  
열거형(Enumerations)은 어떤 값이 이름이 있는 상수 집합에 속한 값 중 하나일 수 있도록 제한하는 기능이다.  
<br />

#### 숫자형 enum
이넘에서 값을 세팅하지 않으면 값이 0부터 세팅된다.  
![Untitled (8)](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/9625bc73-e496-462e-981f-c3e5beef41f7)
<br />  
![Untitled (9)](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/27e6c409-a822-4bf7-b477-db6db8b02c4a)
<br />

값을 설정한 경우, 설정한 숫자부터 순차적으로 1씩 증가한다.  
![Untitled (10)](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/7e1f942c-4291-4212-80c9-1dafb4e0d43d)
<br />  
![Untitled (11)](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/50d3a686-1e98-40c6-a065-33df542330b7)
<br />

#### 문자형 enum
{% highlight ts %}
enum Shoes {
  Nike = "나이키",
  Adidas = "아디다스",
}

let myShoes = Shoes.Nike;
console.log(myShoes); // 나이키
{% endhighlight %} 
<br />

#### enum 활용 예시
드롭다운에서 사용하면 오류를 줄일 수 있음
{% highlight ts %}
enum Answer = {
	Yes = 'Y',
	No = 'N'
}

function askQuestion(answer: Answer){
	if(answer === Answer.Yes){
		console.log('정답입니다');
	}
	if(ansewr === Answer.No) {
		console.log('오답입니다');
	}
}

askQuestion(Answer.Yes);
askQuestion('Yes')
{% endhighlight %} 
<br />

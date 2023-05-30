---
layout: post
title: Typescript의 everyday type(3)
image: typescript_logo.png
excerpt: 
  typescript의 기본 타입
categories: typescript
category: typescript
tags: [타입스트립트, typescript, 타입]
---
✔️ [타입스크립트 핸드북 사이트](https://www.typescriptlang.org/ko/docs/handbook/2/everyday-types.html#%EC%9C%A0%EB%8B%88%EC%96%B8-%ED%83%80%EC%9E%85)

### 유니온 타입

유니언 타입은 서로 다른 두 개 이상의 타입들을 사용하여 만드는 것으로, 유니언 타입의 값은 타입 조합에 사용된 타입 중 무엇이든 하나를 타입으로 가질 수 있다.  
유니온 타입은 세로 막대로 표현되며, "A 또는 B"와 같은 의미를 가진다.  
조합에 사용된 각 타입을 유니언 타입의 멤버라고 부른다.  

예를 들어, 아래 예시에서 **printId** 함수는 **number** 또는 **string** 타입의 인수를 받을 수 있다.
{% highlight ts %}
function printId(id: number | string) {
  console.log("Your ID is: " + id);
}

printId(123);      // 유효한 인수
printId("abc");    // 유효한 인수
printId(true);     // 유효하지 않은 인수 (boolean은 유니온 타입에 포함되지 않음)
{% endhighlight %}
<br />

아래 코드는 에러가 발생한다.
파라미터 id는 number 또는 string 타입이 들어올 수 있는데 number 타입이 들어오면 toUpperCase() 메소드를 사용할 수 없다.  
따라서 유니온 타입에 속하는 값들은 공통된 속성과 메서드만 사용할 수 있다.  
{% highlight ts %}
function printId(id: number | string) {
  console.log(id.toUpperCase());
}
{% endhighlight %}

만약 특정 타입에만 있는 속성이나 메서드를 사용하려고 한다면 코드상에서 유니언을 좁혀야 한다.  
<br />

#### typeof를 활용하여 타입 단언하기
TypeScript는 오직 string 값만이 typeof 연산의 결괏값으로 "string"을 가질 수 있다는 것을 알고 있다.
{% highlight ts %}
function printId(value: string | number) {
  if (typeof value === "string") {
    // value를 string 타입으로 간주하여 length 속성 사용
    console.log(value.length);
  } else {
    console.log("숫자 타입입니다.");
  }
}

printLength("Hello");  // 출력: 5
printLength(123);      // 출력: "숫자 타입입니다."
{% endhighlight %}

---

### 타입 별칭

새로운 이름을 지정하여 기존 타입을 참조하는 것을 의미한다.  
타입 별칭을 사용하면 단지 객체 타입뿐이 아닌 모든 타입에 대하여 새로운 이름을 부여할 수 있다.  

{% highlight ts %}
type User = {
  id: number;
  name: string;
  age: number;
};
const currentUser: User = {
  id: 123,
  name: "Alice",
  age: 25,
};

type ID = number | string;
const userId: ID = '0001'; 
{% endhighlight %}
<br />

타입 별칭에도 제네릭을 사용할 수 있다.
{% highlight ts %}
type User<T> = {
	name: T
}
{% endhighlight %}

---

### 인터페이스

객체의 구조를 정의하는 방법 중 하나로 객체의 필드와 메서드를 설명하는데 사용한다.

{% highlight ts %}
interface Point {
  x: number;
  y: number;
}
 
function printCoord(pt: Point) {
  console.log("The coordinate's x value is " + pt.x);
  console.log("The coordinate's y value is " + pt.y);
}
 
printCoord({ x: 100, y: 100 });
{% endhighlight %}
<br/>

TypeScript는 오직 printCoord에 전달된 값의 구조에만 관심을 가지므로 예측된 프로퍼티만을 가졌다면 오류가 발생하지 않는다.
<br/>

---

### 인터페이스 VS 타입 별칭

인터페이스와 다르게 타입 별칭은 브리뷰에서 프로퍼티들을 자세히 보여주기 때문에 가독성이 더 좋다.
타입은 새 프로퍼티를 추가하도록 개방될 수 없는 반면, 인터페이스의 경우 항상 확장될 수 있다.  
따라서 타입보다 인터페이스를 사용하는 것이 더 좋다.

|  | 인터페이스 | 타입 |
| --- | --- | --- |
|  프로퍼티 프리뷰  |  x  |  o  |
|  확장  |  o  |  x  |

{% highlight ts %}
interface PersonInterface {
  name: string;
  age: number;
}

let dayoung: PersonInterface = {
  name: "dayoung",
  age: 28,
};

type PersonType = {
  name: string;
  age: number;
};

let capt: PersonType = {
  name: "capt",
  age: 30,
};
{% endhighlight %}

![Untitled (6)](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/4671e7cf-cb2a-4d35-b9b5-eda86003ace0)
<br />
![Untitled (7)](https://github.com/DaYoung-woo/DaYoung-woo.github.io/assets/131967254/b84ce8fa-3d2d-46c1-9177-33a3a167b316)

<br/>

#### 인터페이스 확장하기
{% highlight ts %}
interface Animal {
  name: string
}

interface Bear extends Animal {
  honey: boolean
}

const bear = getBear()
bear.name
bear.honey
{% endhighlight %}  
<br/>

#### 교집합을 통하여 타입 확장하기
{% highlight ts %}
type Animal = {
  name: string
}

type Bear = Animal & {
  honey: Boolean
}

const bear = getBear();
bear.name;
bear.honey;
{% endhighlight %}
<br/>

#### 기존의 인터페이스에 새 필드를 추가하기
{% highlight ts %}
interface Window {
  title: string
}

interface Window {
  ts: TypeScriptAPI
}

const src = 'const a = "Hello World"';
window.ts.transpileModule(src, {});    
{% endhighlight %}
<br/>

#### 타입은 생성된 뒤에는 달라질 수 없다
{% highlight ts %}
type Window = {
  title: string
}

type Window = {
  ts: TypeScriptAPI
}

 // Error: Duplicate identifier 'Window'.   
{% endhighlight %}
<br/>


---

### 타입 단언

 "내가 이 값의 타입을 정확히 알고 있으니, 해당 타입으로 취급해주세요"라고 알려주는 방법이다.  

예를 들어 코드상에서 document.getElementById가 사용되는 경우  
나는 페이지 상에서 사용되는 ID로는 언제나 HTMLCanvasElement가 반환된다는 사실을 이미 알고 있다.  
하지만 TypeScript는 이때 HTMLElement 중에 무언가가 반환된다는 것만을 알 수 있다.
이런 경우, 타입 단언을 사용하면 타입을 좀 더 구체적으로 명시할 수 있다.

{% highlight ts %}
const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;
{% endhighlight %}
<br />

TypeScript에서는 보다 구체적인 또는 덜 구체적인 버전의 타입으로 변환하는 타입 단언만이 허용된다.
{% highlight ts %}
const x = "hello" as number;
// Conversion of type 'string' to type 'number' may be a mistake because neither type sufficiently overlaps with the other. 
// If this was intentional, convert the expression to 'unknown' first.
{% endhighlight %}
<br />

타입 단언은 컴파일러에게 추가적인 정보를 제공할 뿐이지, 실제로 값의 타입을 변환시키지는 않는다는 점의 주의해야 한다.  
따라서 잘못된 타입 단언을 사용하면 런타임 에러가 발생할 수 있다.  
해당 값이 실제로 지정한 타입과 호환되는지 확인하는 것이 중요하다.  
{% highlight ts %}
let value: any = "Hello, TypeScript!";
let length: number = (value as number).length;  // 잘못된 타입 단언

console.log(length);
{% endhighlight %}
<br />

또한, 타입 단언은 컴파일 시간에 제거되므로, 타입 단언에 관련된 검사는 런타임 중에 이루어지지 않는다.  
타입 단언이 틀렸더라도 예외가 발생하거나 null이 생성되지 않는다.
{% highlight ts %}
// status란 id를 가진 div가 없을 경우 undefined가 반환된다.
const el = document.getElementById('status') as HTMLDivElement 
el.textContent = 'Ready';
{% endhighlight %}  

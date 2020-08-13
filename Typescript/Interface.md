# 소개

기존의 Javascript에는 Interface라는 개념이 없었다. 하지만 Typescript를 쓰면서 Interface를 사용할 수 있게 되었다. 지금껏 Javascript로 개발한 사람들에게는 interface 개념이 익숙하지 않을 것이다.  
그렇다면 Interface의 개념에 대해 잡고 넘어가보자.  
Interface란 어떠한 두 개의 시스템 사이에 상호작용할 수 있게 해주는 조건, 규약 같은 것이다.  
예를 들어, `타이핑`이라는 Interface가 있다고 해보자. 키보드 'k'를 누르면 알파벳 'k'가 출력된다. 이것은 키보드를 눌렀을 때 어떠한 문자가 출력된다는 `타이핑` Interface를 지키고 있는 것이다.

### Interface는 어떻게 쓰일까?

Interface가 어떻게 동작하는지 코드를 보면서 살펴보도록 하자.

```
function createKeyboard(orderSheet: { ingredient: string, keyCount: number }) {
    console.log(`키보드 만드는중...`);
}
let orderSheet = {
    ingredient: 'plastic',
    keyCount: 40,
};
createKeyboard(orderSheet);
```

여기에 키보드를 만드는 함수가 있다. 이 함수는 주문서를 받는데 그 주문서에 적혀있는 내용은 성분인 ingredient, 그리고 키보드 키의 개수인 keyCount 라는 항목이 있고 이 두 개를 적어줘야 만들 수 있다.

그런데 만약 주문서에 작성할 내용이 엄청 많아지면 코드가 너무 지저분해질것이 분명하다. 이 때 타입스크립트의 interface 를 사용한다.  
아래 코드는 인터페이스를 사용했을 때의 코드이다.

```
interface OrderSheet {
    ingredient: string;
    keyCount: number;
}
function createKeyboard(orderSheet: OrderSheet) {
    console.log(`키보드 만드는중...`);
}
```

확실히 가독성이 더 좋아진것을 볼 수 있다. 그리고 주문서의 항목란이 많아질 경우에도 문제가 없을것 같다.

### 선택적 프로퍼티란?

이름을 새기는 각인이라는 항목이 주문서에 추가가 되었다. 하지만 이 각인은 고객이 이름을 적어주었을 경우에만 새겨야 한다. 이렇게 **선택적으로 어떠한 옵션을 주어야할 때** `선택적 프로퍼티`를 이용한다. 프로퍼티 이름의 끝에 `?` 만 넣어주면 된다.

```
interface OrderSheet {
    ingredient: string;
    keyCount: number;
    name?: string;
}
function createKeyboard(orderSheet: OrderSheet) {
    console.log(`키보드 만드는중...`);
}
let orderSheet1 = {
    ingredient: 'plastic',
    keyCount: 40,
};
let orderSheet2 = {
    ingredient: 'metal',
    keyCount: 30,
    name: 'heecheolman',
};
createKeyboard(orderSheet1);
createKeyboard(orderSheet2);
```

### 읽기전용 프로퍼티는 뭘까?

주문을 했는데 고객이 각인될 내용을 바꾸고 싶다고 한다면(?), 만약 주문이 들어가면 바꿀 수 없는 시스템이라 가정을 했을 때는 읽기전용으로 하고싶은 프로퍼티앞에 readonly 만 붙여주면 된다.

```
interface OrderSheet {
    ingredient: string;
    keyCount: number;
    readonly name?: string;
}
function createKeyboard(orderSheet: OrderSheet) {
    console.log(`키보드 만드는중...`);
    // orderSheet.name = 'heecheol';
    // Error : TS2540: Cannot assign to 'name' because it is a read-only property.
}
```

`readonly` 는 `const` 와 동일한 역할을 수행한다. **변수일 경우엔 const** 를 사용하고 **프로퍼티일 경우에는 readonly** 로 사용하면 된다.

추가적으로 배열을 읽기전용으로 하고싶다면 `Readonly<type>` 으로 선언을 해준다.

```
let keyElements: ReadonlyArray<string> = ['a', 'b', 'c', 'd'];
let newKeyElements: string[];
// Errors!
// keyElements.push(1);
// keyElements[0] = 'A';
// let temp: string[] = keyElements;
// newKeyElements = keyElements;
// Ok!
newKeyElements = keyElements as string[];
newKeyElements.push('e');
```

push, 인덱스 접근 후 할당, 새로운 string 배열인 temp 에 할당같은 것들이 전부 불가능하지만 Type Assertion 을 이용하면 가능합니다.

### 함수 타입

Interface의 프로퍼티로 함수 시그니처를 정의할 수 있다.

시그니처란?  
MDN 웹 문서에 따르면, functions 그리고 method의 입력과 출력을 정의한다.  
시그니처는 다음을 포함한다.

- parameters 와 그들의 types

- 반환값과 타입

- 던져지거나 콜백으로 반환되는 exceptions

- OOP 에서 메서드의 접근 권한에 대한 정보(public, static, 혹은 prototype와 같은 키워드들)

  ```
  interface TypingSpec {
    (sound: string, weight: number): boolean;
  }
  const checkCreatedKeyboard: TypingSpec = (s: string, w: number): boolean => w < 10;
  console.log(checkCreatedKeyboard('took', 11)); // false;
  console.log(checkCreatedKeyboard('tok', 3)); // true
  ```

  위의 코드에서는 만들어진 키보드를 체크하는 인터페이스에는 sound(누르는 소리) 와 weight(누르는 가중치)를 파라미터로 받는다. 만약 누르는 힘이 10 이상 든다면 제품을 쓸 수 없다고 가정했다.

인터페이스 프로퍼티로 정해준 함수 시그니쳐의 파라미터의 이름과 구현하는 부분의 파라미터 이름이 꼭 동일할 필요는 없다. s 와 w 로 정해준것을 확인할 수 있다.

### Indexable 타입

#### Indexable 타입 예제

```
interface StringArray {
  [index: number]: string;
}
let myArray: StringArray;
myArray = ['bob', 'fred'];
let myStr: string = myArray[0];
console.log(myStr); // bob
```

`StringArray`가 `number`로 인덱스 될 때 string을 리턴한다.

#### 자바스크립트 Index의 동작방식

타입스크립트로 들어가기전에 자바스크립트의 객체 프로퍼티에 접근하는 방법을 살펴보자. 자바스크립트는 객체의 프로퍼티에 접근 할 때 문자열로 접근할 수 있다. \[\]를 이요하여 접근이 가능하다.

```
// ES6
let obj = {};
obj['str'] = 'string';
console.log(obj['str']); // string
```

그리고 객체로도 객체의 프로퍼티를 지정할 수 있다

```
// ES6
let obj = {};
let foo = {};
foo[obj] = 'Key is obj';
console.log(foo[obj]); // Key is obj
```

**자바스크립트 Index의 동작방식에 의해 객체의 Index에 접근할 때 내부적으로 toString() 메서드를 호출하여 문자열로 변형된 값을 통해 접근한다.**

```
// ES6
let obj = {
  toString() {
    console.log('toString() called');
  }
};
let foo = {};
foo[obj] = 'Key is obj'; // toString() called
console.log(foo[obj]);
// toString() called
// Key is obj
```

toString() 메서드를 호출해 문자열로 바뀌는 것을 콘솔로 확인했다. 위의 예제에서는 toString() 에 대한 로그를 두 번 호출하는데 그 이유는 접근 할 때마다 toString() 이 호출되기 때문이다.

#### Indexable 사용법

자바스크립트에서 사용하듯 타입스크립트에서 객체를 하나 만들어보자.

```
// ES6
const obj = {
  a: '에이',
  b: '비',
};
Object.keys(obj.forEach(key => console.log(obj[key]));
```

하지만 이 코드는 타입스크립트에서는 에러를 발생시킨다.

```
TS7017: Element implicitly has an 'any' type because type '{ a: string; b: string; }' has no index signature.
```

index signature가 없다는 에러메시지가 보인다. 왜냐하면 프로퍼티에 접근할 때 어떤 타입인지 확인할 수 없어 암묵적으로 any 타입을 사용하기 때문이다.

> 이는 tsconfig의 "noImplicitAny": true 이기 때문에 발생하는 에러이다.  
> noImplicitAny의 default는 true 이다.

**해결 방법은 index signature 를 사용하면 된다.**

다음 예제의 index signature의 의미는 key 값은 string이고 반환 값도 string이다 라는 뜻이다.

```
// TS
interface IndexSignature {
  [key: string]: string;
}
const obj: IndexSignature = {
  a: '에이',
  b: '비',
};
Object.keys(obj).forEach(key => console.log(obj[key]));
```

#### 주의해야할 점

1.  index signature의 타입은 문자열 또는 숫자만 가능하다.

    ```
    // TS
    // Error!
    interface Interface {
    ```

}  
// TS1023: An index signature parameter type must be 'string' or 'number'.

````

2. 문자열 Index와 숫자 Index가 모두 존재할 경우, 숫자로 된 Index의 값의 타입은 문자열로 Indexing된 값 타입의 서브타입이어야 한다.
```ts
// TS
class Animal {
  name: string;
}
class Dog extends Animal {
  breed: string;
}
// Error: '문자열'로 Index를 생성하면 가끔 'Dog'가 생긴다.
interface NotOkay {
  [x: number]: Animal;
  [x: string]: Dog;
}
````

위의 코드가 에러인 이유는 처음에 말씀드렸던 자바스크립트가 색인을 할 때 toString() 을 먼저 호출하기 때문이다. 가령, obj\[1\] 로 접근을 하면 우리가 기대했던 Animal 이 값으로 나올 것 같지만 1 은 문자열 '1' 로 변환이 되기 때문에 Dog 가 나올수도 있다는 예제이다.

#### 유니온 타입을 이용한 Index signature

```
// TS
interface UnionTypeSignature {
  [key: string]: number | string;
  name: string;
  age: number;
}

const me: UnionTypeSignature = {
  name: 'kevin kim',
  age: 30,
};
console.log(me.name); // kevin kim
console.log(me.age); // 30
console.log(me['name']); // kevin kim
console.log(me['age']); // 30
```

유니온 타입을 이용하려면 인덱서는 그 아래 프로퍼티의 속성들을 모두 가지고 있어야 한다.

#### 제한된 리터럴 문자열 셋

매핑된 유형을 사용해 index signature 가 문자열 조합의 구성원이어야만 사용할 수 있게끔 제약할 수 있다.

```
// TS
type Index = 'a' | 'b' | 'c';
type FromIndex = {
  [k in Index]?: number;
}
const good: FromIndex = {
  a: 1,
  b: 1,
  c: 3,
};
/* TS2322: Type '{ b: number; c: number; d: number; }' is not assignable to type 'FromIndex'.
Object literal may only specify known properties, and 'd' does not exist in type 'FromIndex'. */
const bad: FromIndex = {
  b: 2,
  c: 3,
  d: 4, // Error
};
// d 속성이 없기 때문이다.
```

#### 중첩된 Index Signature

```
// TS
interface NestedCSS {
  color?: string;
  [selector: string]: string | NestedCSS;
}
const example: NestedCSS = {
  color: 'black',
  '.subclass': {
    color: 'white',
  },
};
```

이렇게 했을 경우 다음과 같은 오타를 잡지 못한다.

```
// TS
const failsSiently: NestedCSS = {
  colour: 'gold',
};
```

해결책은 다음과 같다. nest, children, subnodes 등등과 같은 이름을 갖는 프로퍼티를 만들고 그 안에 내장시킨다.

```
// TS
interface NestedCSS {
  color?: string;
  nest?: {
    [selector: string]: NestedCSS;
  };
}
const example: NestedCSS = {
  color: 'black',
  nest: {
    '.subclass': {
      color: 'white',
    }
  }
};
```

이제 다음과 같은 코드는 에러를 뱉는다.

```
// TS
const failsSiently: NestedCSS = {
  colour: 'gold',
};
/*
TS2322: Type '{ colour: string; }' is not assignable to type 'NestedCSS'.
 Object literal may only specify known properties, but 'colour' does not exist in type 'NestedCSS'. Did you mean to write 'color'?
*/
```

#### NestedDom

다음의 코드는 위의 NestedCSS를 응용해 짜여진 코드이다.

```ts
// TS
interface NestedDOM {
	tag: string;
	textNode?: string;
	children?: NestedDOM[];
}
```

NestedDOM 인터페이스를 구현한 객체이다.

```ts
// TS
const domGroup: NestedDOM = {
	tag: 'div',
	children: [
		{
			tag: 'h1',
			textNode: 'Introduction',
		},
		{
			tag: 'ul',
			children: [
				{
					tag: 'li',
					children: [
						{
							tag: 'text',
							textNode: 'Hello',
						},
					],
				},
				{
					tag: 'li',
					children: [
						{
							tag: 'text',
							textNode: 'kevin kim',
						},
					],
				},
				{
					tag: 'li',
					children: [
						{
							tag: 'text',
							textNode: 'World!',
						},
					],
				},
			],
		},
	],
};
```

위의 코드는 HTML로 아래처럼 표기된다.

```js
<div>
	<h1>Introduction</h1>
	<ul>
		<li>Hello</li>
		<li>kevin kim</li>
		<li>World!</li>
	</ul>
</div>
```

아래는 NestDOM을 파싱하는 createComponent() 함수이다.

```ts
function createComponent(
	domGroup: NestedDOM,
	closeTags: string[] = [],
	nodes: string = '',
): string {
	let nodeString: string = nodes || '';
	let cTags: string[] = closeTags || [];
	if (typeof domGroup !== 'object' || !domGroup) {
		while (cTags.length !== 0) {
			nodeString += cTags.pop();
		}
		return nodeString;
	}
	const tag = domGroup.tag;
	nodeString += `<${tag}>`;
	cTags.push(`</${tag}>`);
	if (domGroup.textNode) {
		nodeString += domGroup.textNode;
	}
	if (domGroup.children) {
		domGroup.children.forEach(child => {
			nodeString = createComponent(child, cTags, nodeString);
		});
	} else {
		nodeString += cTags.pop();
		return nodeString;
	}
	return nodeString;
}
document.body.innerHTML = createComponent(domGroup);
```

#### readonly 프로퍼티

```ts
// TS
interface ReadonlyStringArray {
	readonly [index: number]: string;
}
let myArray: ReadonlyStringArray = ['Alice', 'Bob'];
myArray[2] = 'Mallory'; // error!
```

readonly 를 앞에 붙이게되면 읽기전용이 된다.

## 클래스 타입

클래스에서도 Interface를 사용할 수 있다. 클래스에서는 implements 라는 키워드를 통해 구현한다.

```ts
// TS
interface ClockInterface {
	currentTime: Date;
}
class Clock implements ClockInterface {}
```

위의 코드는 아래와 같은 에러를 뱉는다.

```js
TS2420: Class 'Clock' incorrectly implements interface 'ClockInterface'.
 Property 'currentTime' is missing in type 'Clock' but required in type 'ClockInterface'.
```

**implements 라는 키워드가 있다면 해당 Interface를 무조건 구현해야 한다.**  
또한 Interface를 구현하는 클래스는 public 만을 사용할 수 있는데 그 이유는 private 로 구현을 하면 Interface를 구현했는지 안했는지 모르기 때문이다.

추가적으로 Interface를 구현한 클래스의 타입은 인터페이스가 될 수 있다.

```ts
// TS
interface ClockInterface {
	currentTime: Date;
}
class Clock implements ClockInterface {
	public currentTime: Date;
	// private _currentTime: Date; // Error!
}
const digital: ClockInterface = new Clock();
```

## 확장 interface

Interface도 클래스처럼 extends 키워드를 통해 확장할 수 있다. Interface를 분리함으로써 재사용성이 뛰어나다.

```ts
// TS
interface DOM {
	display: string;
	tag: string;
}
interface TextNode extends DOM {
	text: string;
}
interface InputNode extends DOM {
	type: string;
}
const textNode: TextNode = {
	display: 'inline',
	tag: 'text',
	text: 'heecheolman',
};
const InputNode: InputNode = {
	display: 'inline-block',
	tag: 'input',
	type: 'button',
};
```

## Hybrid 타입

자바스크립트의 프로퍼티에는 함수도 포함될 수 있다. 확장 Interface에서의 예제를 응용해본다면 InputNode 는 click 메서드를 통해 사용자의 이벤트를 받을 수 있어야할 것 같다. 그렇다면 아래의 코드처럼 짤 수 있다.

```ts
// TS
// ... 생략
type eventDOM = object;
interface InputNode extends DOM {
	type: string;
	click(eventDOM: object): void;
}
const InputNode: InputNode = {
	display: 'inline-block',
	tag: 'input',
	type: 'button',
	click(eventDOM: object) {
		console.log(`${eventDOM} was clicked!`);
	},
};
```

click 이라는 메서드는 DOM 을 받아서 클릭이벤트를 수행한다.  
`type eventDOM = object` 를 통해 click() 메서드의 파라미터에 대한 타입을 명시적으로 잡아주었다.

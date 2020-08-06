# 소개

기존의 Javascript에는 Interface라는 개념이 없었다. 하지만 Typescript를 쓰면서 Interface를 사용할 수 있게 되었다. 지금껏 Javascript로 개발한 사람들에게는 interface 개념이 익숙하지 않을 것이다.
그렇다면 Interface의 개념에 대해 잡고 넘어가보자.
Interface란 어떠한 두 개의 시스템 사이에 상호작용할 수 있게 해주는 조건, 규약 같은 것이다.
예를 들어, `타이핑`이라는 Interface가 있다고 해보자. 키보드 'k'를 누르면 알파벳 'k'가 출력된다. 이것은 키보드를 눌렀을 때 어떠한 문자가 출력된다는 `타이핑` Interface를 지키고 있는 것이다.

### Interface는 어떻게 쓰일까?

Interface가 어떻게 동작하는지 코드를 보면서 살펴보도록 하자.

```ts
function createKeyboard(orderSheet: { ingredient: string; keyCount: number }) {
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

```ts
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

```ts
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

### 함수 타입에 대해 알아보자.

Interface의 프로퍼티로 함수 시그니처를 정의할 수 있다.

시그니처란?
MDN 웹 문서에 따르면, functions 그리고 method의 입력과 출력을 정의한다.
시그니처는 다음을 포함한다.

- parameters 와 그들의 types
- 반환값과 타입
- 던져지거나 콜백으로 반환되는 exceptions
- OOP 에서 메서드의 접근 권한에 대한 정보(public, static, 혹은 prototype와 같은 키워드들)

```ts
interface TypingSpec {
	(sound: string, weight: number): boolean;
}
const checkCreatedKeyboard: TypingSpec = (s: string, w: number): boolean =>
	w < 10;
console.log(checkCreatedKeyboard('took', 11)); // false;
console.log(checkCreatedKeyboard('tok', 3)); // true
```

위의 코드에서는 만들어진 키보드를 체크하는 인터페이스에는 sound(누르는 소리) 와 weight(누르는 가중치)를 파라미터로 받는다. 만약 누르는 힘이 10 이상 든다면 제품을 쓸 수 없다고 가정했다.

인터페이스 프로퍼티로 정해준 함수 시그니쳐의 파라미터의 이름과 구현하는 부분의 파라미터 이름이 꼭 동일할 필요는 없다. s 와 w 로 정해준것을 확인할 수 있다.

### Indexable 타입에 대해 알아보자.

Indexable 타입 예제

```ts
interface StringArray {
	[index: number]: string;
}
let myArray: StringArray;
myArray = ['bob', 'fred'];
let myStr: string = myArray[0];
console.log(myStr); // bob
```

StringArray가 number로 인덱스 될 때 string을 리턴한다.

Javascript Index의 동작방식
타입스크립트로 들어가기 전에 자바스크립트의 객체 프로퍼티를 접근하는 방법을 살펴보자. 자바스크립트는 객체의 프로퍼티에 접근할 때 문자열로 접근할 수 있다. []를 사용해 접근이 가능하다.

```js
let obj = {};
obj['str'] = 'string';
console.log(obj['str']); // string
```

그리고 객체로도 객체의 프로퍼티로 지정할 수 있다.

```js
let obj = {};
let foo = {};
foo[obj] = 'Key is obj';
console.log(foo[obj]); // Key is obj
```

**자바스크립트 Index의 동작방식에 의해 객체의 Index에 접근할 때 내부적으로 toString() 메서드를 호출하여 문자열로 변형된 값을 통해 접근한다.**

```js
let obj = {
	toString() {
		console.log('toString() called');
	},
};
let foo = {};
foo[obj] = 'Key is obj'; // toString() called
console.log(foo[obj]);
// toString() called
// Key is obj
```

toString() 메서드를 호출해 문자열로 바뀌는것을 콘솔로 확인했다. 위의 예제에서는 toString() 에 대한 콘솔로그를 두번 호출하는데 그 이유는 접근할 때마다 toString() 이 호출되기 때문이다.

> 자바스크립트는 동적타입 언어이다. 변수의 타입 지정 없이 할당되는 과정에서 자동으로 변수의 타입이 결정된다.
> 즉, 변수는 고정된 타입이 없다. 따라서 같은 변수에 여러 타입의 값을 자유롭게 할당할 수 있다.
>
```js
var str  = 'Hello';
var num  = 1;
var bool = true;
 
var foo = 'string';
console.log(typeof foo); // string
foo = 1;
console.log(typeof foo); // number
```

## 1. 데이터 타입
> 데이터 타입은 프로그래밍 언어에서 사용할 수 있는 데이터(숫자, 문자열, 불리언)의 종류를 말한다.
> 자바스크립트의 모든 값은 데이터 타입 값을 갖는다. `ECMAScript 표준(ES6)은 7개의 데이터 타입을 제공`한다.
> * 원시 타입(primitive data type)
>
> boolean, null, undefined, number, string, symbol
>
> 원시 타입의 값은 `변경 불가능한 값`이며 `pass-by-value(값에 의한 전달)`이다.
>
> * 객체 타입(object/reference type)
>
> object
>
>
>1-1. `Document.querySelector()` => `조건에 부합하는 HTML요소를 검색해 반환`
```js
var element = document.querySelector('.myElem');
// HTML 문서에 myElem 클래스를 갖는 요소가 없다면 null을 반환한다.
console.log(element); // null
```

>1-2. `typeof` 연산자 => `타입을 나타내고 문자열을 반환`
```js
var foo = null;
console.log(typeof foo === null); // false
console.log(foo === null);        // true
```

>1-3. 동적타이핑 : 자바스크립트는 동적타입언어이다. 이것은 변수의 타입 지정 없이 값이 할당되는 과정에서
>값의 타입에 의해 자동으로 타입이 결정될 것이라는 뜻이다. 따라서 같은 변수에 여러 타입의 값을 할당할 수 있다.
>이를 `동적 타이핑`이라고 한다.
```js
var foo;

console.log(typeof foo);  // undefined

foo = null;
console.log(typeof foo);  // object

foo = {};
console.log(typeof foo);  // object

foo = 3;
console.log(typeof foo);  // number

foo = 3.14;
console.log(typeof foo);  // number

foo = 'Hi';
console.log(typeof foo);  // string

foo = true;
console.log(typeof foo);  // boolean
```

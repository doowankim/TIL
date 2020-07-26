# Boolean

> 가장 기본적인 데이터 타입은 Javascript, Typescript에서 `boolean` 값이라고 일컫는 참/거짓(true/false) 값이다.

```ts
let isDone: boolean = false;
```

# Number (숫자)

> Javascript 처럼, Typescript의 모든 숫자는 부동 소수 값이다. 부동 소수에는 `number`라는 타입이 붙여진다. Typescript에는 16진수, 10진수 리터럴에 더불어, ECMAScript 2015에 소개된 2진수, 8진수 리터럴도 지원한다.

```ts
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
```

# String (문자열)

> 웹 페이지, 서버 같은 프로그램을 Javascript로 만들 때 기본적으로 텍스트 데이터를 다루는 작업이 필요하다. 다른 언어들처럼 Typescript에서는 텍스트 데이터 타입을 `string`으로 표현한다. Javascript처럼 Typescript도 큰따옴표 ("")나 작은 따옴표('')를 문자열 데이터를 감싸는데 사용한다.

```ts
let color: string = 'blue';
color: 'red';
```

> 또한 템플릿 문자열을 사용하면 여러 줄에 걸쳐 문자열을 작성할 수 있으며, 표현식을 포함시킬 수도 있다. 이 문자열은 백틱/백쿼트(``)를 사용하며, `${expo}`와 같은 형태로 표현식을 포함시킬 수 있다.

```ts
let fullname: string = `Bob Bobbington`;
let age: number = 37;
let sentence: string = `Hello, my name is ${fullname}.
I'll be ${age + 1} years old next month.`;
```

위에서 백틱을 사용하여 여러 줄에 걸친 문자열을 작성했다면, 아래는 따옴표를 이용하여 여러 줄을 작성한 것이다.

```ts
let sentence: string = "Hello, my name is " + fullname + ".\n\n" +
"I'll be " + (age + 1) + " years old next month.".
```

# Array (배열)

> Typescript는 Javascript처럼 값들을 배열로 다룰 수 있게 해준다. 배열 타입은 두 가지 방법으로 사용할 수 있다. 첫 번째 방법은, 배열 요소들을 나타내는 타입 뒤에 `[]`를 쓰는 것이다.

```ts
let list: number[] = [1, 2, 3];
```

> 두 번째 방법은, `제네릭 배열 타입`을 쓰는 것이다. `Array<elemType> :`

```ts
let list: Array<number> = [1, 2, 3];
```

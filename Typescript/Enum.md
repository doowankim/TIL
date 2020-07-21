## 열거형 타입(enum)

열거형 타입은 enum 키워드를 사용해서 정의한다. 열거형 타입의 각 원소는 `값`으로 사용될 수 있고, `타입`으로 사용될 수도 있다. 아래의 코드를 보자.

```ts
enum Fruit {
	Apple,
	Banana,
	Orange,
}
const v1: Fruit = Fruit.Apple;
const v2: Fruit.Apple | Fruit.Banana = Fruit.Banana;
```

```ts
enum Fruit {
	Apple,
	Banana,
	Orange,
}
```

위의 코드는 열거형 타입을 이용해서 과일을 정의했다.

```ts
const v1: Fruit = Fruit.Apple;
```

위의 코드는 열거형 타입의 원소인 Apple을 값으로 사용했다.

```ts
const v2: Fruit.Apple | Fruit.Banana = Fruit.Banana;
```

위의 코드는 Apple을 타입으로 사용했다.

다음은 명시적으로 원소의 값을 입력하는 코드를 살펴보자.

```ts
enum Fruit {
	Apple,
	Banana = 5,
	Orange,
}
console.log(Fruit.Apple, Fruit.Banana, Fruit.Orange); // 0, 5, 6
```

열거형 타입의 첫 번째 원소에 값을 할당하지 않으면 자동으로 0이 할당된다.(Apple, Orange)
열거형 타입의 각 원소에 숫자 또는 문자열을 할당할 수 있다. **명시적으로 값을 입력하지 않으면 이전 원소에서 `1만큼 증가한 값`이 할당된다.**

다른 타입과 달리 열거형 타입은 컴파일 후에도 관련된 코드가 남는다. 예를 들어, 타입스크립트는 아래와 같이 컴파일한다.

```ts
let Fruit;
(function (Fruit) {
	Fruit[(Fruit['Apple'] = 0)] = 'Apple';
	Fruit[(Fruit['Banana'] = 5)] = 'Banana';
	Fruit[(Fruit['Orange'] = 6)] = 'Organge';
})(Fruit || (Fruit = {}));
console.log(Fruit.Apple, Fruit.Banana, Fruit.Orange); // 0, 5, 6
```

- 열거형 타입은 객체로 존재한다 => `(Fruit || (Fruit = {}));`
- 열거형 타입의 각 원소는 이름과 값이 양방향으로 매핑(mapping)된다.
  => `Fruit[(Fruit['Apple'] = 0)] = 'Apple';`

열거형 타입은 객체로 존재하기 때문에 해당 객체를 런타임에 사용할 수 있다. 다음은 **열거형 타입의 객체를 사용하는 코드**를 알아보자.

```ts
enum Fruit {
	Apple,
	Banana = 5,
	Orange,
}
console.log(Fruit.Banana); // 5
console.log(Fruit['Banana']); // 5
console.log(Fruit[5]); // Banana
```

6, 7행의 코드를 보면, 열거형 타입은 객체이기 때문에 일반적인 객체처럼 다룰 수 있다.
8행의 코드를 보면, 각 원소의 이름과 값이 양방향으로 매핑되어 있기 때문에 값을 이용해서 이름을 가져올 수 있다.

다음 포스트에서는 enum의 타입을 위한 유틸리티 함수에 대해 공부해보겠다!

# Typescript의 enum

Typescript의 enum은 Javascript에 없는 개념으로, 딱 보면 상수, 배열, 객체와 비슷해보인다. 그렇다면 상수, 배열, 객체를 쓰면 될텐데 왜 굳이 enum을 사용할까?

### enum은 추상화의 수단이다

예를 들어, 다국어 언어 지원을 위해 언어 코드를 저장할 변수를 만들어야 하는 상황이 왔다고 가정해보자.

```ts
const code: string = 'en';
```

위의 코드를 보면 제품이 지원할 수 있는 언어는 사전에 정해져있는데, 이 값이 할당될 변수를 string 타입으로 지정하는 것은 너무 광범위하다고 생각이 든다. 그렇다면 이를 개선해보자.

```ts
type LanguageCode = 'ko' | 'en' | 'ja' | 'zh' | 'es';

const code: LanguageCode = 'ko';
```

일단은 위의 코드처럼 **리터럴 타입**과 **유니온**을 이용해 code 변수에 대한 타입의 범위를 좁혀줄 수 있다.
이제 code 변수에 'zz' 같이 이상한 값을 대입하면 컴파일 에러가 난다. 타입의 범위는 string으로 했을 때 보다 범위가 좁아진 것을 확인할 수 있다.

하지만 일이 진행됨에 따라 제품이 어떤 언어를 지원하기로 했었는지도 가물가물하고, 특정 국가 코드가 정확히 어떤 언어를 가리키는지 일일이 외우기도 쉽지 않다. 이 때 상수를 여러 개 둬서 문제를 해결할 수는 있지만 그닥 깔끔한 느낌은 아니다.

```ts
// 1.
const korean = 'ko';
const english = 'en';
const japanese = 'ja';
const chinese = 'zh';
const spanish = 'es';
```

```ts
// 2.
type LanguageCode = 'ko' | 'en' | 'ja' | 'zh' | 'es';
```

```ts
// 3.
type LanguageCode =
	| typeof korean
	| typeof english
	| typeof japanese
	| typeof chinese
	| typeof spanish;

const code: LanguageCode = korean;
```

세 개의 코드 중에 무엇이 괜찮아 보이는지 선택해보자.
내가 보기에는 첫 번째 코드는 상수를 여러 개를 두었기 때문에 비효율적인 것처럼 보이고, 두 번째 코드는 위에 적은 코드랑 겹친다. 마지막으로 적은 코드는 너무 길어진 것 같아 보기에 좋지 않다.

이런 경우에 enum 타입을 사용해 **리터럴의 타입과 값에 이름을 붙여서 코드의 가독성을 높일 수 있다**.

```ts
export enum LanguageCode {
	korean = 'ko',
	english = 'en',
	japanese = 'ja',
	chinese = 'zh',
	spanish = 'es',
}

const code: LanguageCode = LanguageCode.korean;
```

### enum은 객체이다

Typesciprt의 **enum은 그 자체로 객체**이기도 하다.

```ts
const keys = Object.keys(LanguageCode); // ['korean', 'english', ...]
const values = Object.values(LanguageCode); // ['ko', 'en', ...]
```

그렇다면 그냥 객체와는 어떤 차이점이 있을까?

1. 객체는 별다른 처리를 해주지 않았다면 속성을 자유로이 변경할 수 있는데, **enum의 속성은 변경할 수 없다.**

2. 객체의 속성은 별다른 처리를 해주지 않았다면 리터럴의 타입이 아니라 그보다 더 넓은 타입으로 타입 추론이 이루어진다. 하지만 **enum은 항상 리터럴의 타입이 사용된다.**

3. 객체의 속성 값으로는 Javascript가 허용하는 모든 값이 올 수 있지만, **enum의 속성 값으로는 문자열 또는 숫자만 허용된다.**

## 정리

**같은 ‘종류’를 나타내는 여러 개의 숫자 혹은 문자열을 다뤄야 하는데, 각각 적당한 이름을 붙여서 코드의 가독성을 높이고 싶다면 enum을 사용**하면 된다. 그 외의 경우 상수, 배열, 객체 등을 사용하면 된다.

p.s 또한 Typescript에는 enum의 속성 값을 명시적으로 정해주지 않아도 자동으로 0부터 시작하는 정수들이 지정되는 기능이 있다!

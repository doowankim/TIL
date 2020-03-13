## 조건문

> * 삼항조건 연산자 (if-else 문)
> 
> 일반 if-else 문 : boolean 값으로 평가될 수 있는 표현식, 논리적 참, 거짓에 따라 실행할 코드 블록을 결정한다.
```js
// x가 짝수이면 ‘짝수'를 홀수이면 ‘홀수'를 반환한다.
var x = 2;
var result;

if (x % 2) { // 2 % 2는 0이고 0은 false로 취급된다.
  result = '홀수';
} else {
  result = '짝수';
}

console.log(result); // 짝수
```
>
> 삼항조건 연산자
```js
// x가 짝수이면 '짝수'를 홀수이면 '홀수'를 반환한다.
var x = 2;

// 0은 false로 취급된다.
var result = x % 2 ? '홀수' : '짝수';
console.log(result); // 짝수
```

> * switch 문 : boolean 값보다는 문자열, 숫자 값인 경우가 많음, 논리적인 참, 거짓보다는 다양한 상황(case)에 따라 실행할 코드 블록을 작성할 때 사용된다.
>
```js
switch (표현식) {
  case 표현식1:
    switch 문의 표현식과 표현식1이 일치하면 실행될 문;
    break;
  case 표현식2:
    switch 문의 표현식과 표현식2가 일치하면 실행될 문;
    break;
  default:
    switch 문의 표현식과 일치하는 표현식을 갖는 case 문이 없을 때 실행될 문;
}
```

```js
// 월을 영어로 변환한다. (11 → 'November')
var month = 11;
var monthName;

switch (month) {
  case 1:
    monthName = 'January';
  case 2:
    monthName = 'February';
  case 3:
    monthName = 'March';
  case 4:
    monthName = 'April';
  case 5:
    monthName = 'May';
  case 6:
    monthName = 'June';
  case 7:
    monthName = 'July';
  case 8:
    monthName = 'August';
  case 9:
    monthName = 'September';
  case 10:
    monthName = 'October';
  case 11:
    monthName = 'November';
  case 12:
    monthName = 'December';
  default:
    monthName = 'Invalid month';
}

console.log(monthName); // Invalid month
```
> 위 예제에서 November가 출력되지 않고 Invalid month가 출력되는 이유는 switch 문을 탈출하지 않고 switch문이 끝날 때까지
> 모든 case 문과 default 문을 실행했기 때문이다.
> 이를 폴스루(fall through)라 한다. 다시 말해 변수 monthName에 'November'가 할당된 후, switch 문을 탈출하지 않고
> 연이어 'December'가 재할당되고 마지막으로 'Invalid month'가 재할당되었다.
> 결과가 이러한 이유는 case 문에 해당하는 문 마지막에 `break` 문을 사용하지 않았기 때문이다.
> break 키워드로 구성된 break 문은 코드 블록에서 탈출하는 역할을 수행한다.
> break 문이 없다면 case 문의 표현식과 일치하지 않더라도 실행 순서는 다음 case 문으로 연이어 이동한다.

```js
// 월을 영어로 변환한다. (11 → 'November')
var month = 11;
var monthName;

switch (month) {
  case 1:
    monthName = 'January';
    break;
  case 2:
    monthName = 'February';
    break;
  case 3:
    monthName = 'March';
    break;
  case 4:
    monthName = 'April';
    break;
  case 5:
    monthName = 'May';
    break;
  case 6:
    monthName = 'June';
    break;
  case 7:
    monthName = 'July';
    break;
  case 8:
    monthName = 'August';
    break;
  case 9:
    monthName = 'September';
    break;
  case 10:
    monthName = 'October';
    break;
  case 11:
    monthName = 'November';
    break;
  case 12:
    monthName = 'December';
    break;
  default:
    monthName = 'Invalid month';
}

console.log(monthName); // November
```
>
> default 문에는 break 문을 생략하는 것이 일반적이다. default 문은 switch문의 제일 마지막에 위치하므로 default 문의 실행이 종료되면
switch 문을 빠져나간다. 따라서 별도의 break 문이 필요없다.
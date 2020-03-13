## While 문

> while 문은 주어진 조건식의 평가 결과가 참이면 코드 블록을 계속해서 반복 실행한다. 조건문의 평가 결과가 거짓이 되면
> 실행을 종료한다. 만약 조건식의 평가 결과가 boolean 값이 아니면 boolean 값으로 `강제 변환`되어 논리적 참, 거짓을 구별한다.
```js
var count = 0;
// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
while (count < 3) {
    console.log(count);
    count++;
} // 0 1 2
```
>
> 조건식의 평가 결과가 언제나 참이면 무한루프가 된다.
```js
// 무한루프
while (true){

}
```
>
> 무한루프를 탈출하기 위해서는 코드 블럭 탈출 조건을 if문에 부여하고 break 문으로 코드 블럭을 탈출한다.
```js
var count = 0;
while (true) {
    console.log(count);
    count++;
    
    if (count === 3) break;
} // 0 1 2
```

## do..while 문

> do..while 문은 코드 블록을 실행하고 조건식을 평가한다. 따라서 코드 블록은 무조건 한 번 이상 실행된다.
```js
var count = 0;

// count가 3보다 작을 때까지 코드 블록을 계속 반복 실행한다.
do {
    console.log(count);
    count++;
} while (count < 3); // 0 1 2
```


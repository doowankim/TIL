> 리액트 컴포넌트에서 state는 컴포넌트 내부에서 선언하며, 내부에서 값을 변경할 수 있다.

> state는 동적인 데이터를 사용할 때 사용한다.

```js
import React, { Component } from 'react';

class Counter extends Component {
    state = {
        number: 0
    }

    handleIncrease = e => {
        this.setState({
            number: this.number + 1
        });
    }

    handleDecrease = e => {
        this.setState({
            number: this.number - 1
        });
    }

    render() {
        return (
            <div>
                <div>값: {this.state.number}</div>
                <button onClick={this.handleIncrease}>+</button>
                <button onClick={this.handleDecrease}>-</button>
            </div>
        );
    }
}

export default Counter;
```

> 위의 코드에서 보면 constructor를 사용하지 않았는데, 그 이유는 <b>class fields</b> 문법을 사용했기 때문이다.
> class fields를 사용하는건 편의를 위함이다.
>
> 또한 handleIncrease와 handleDecrease 함수의 내용을 보면 아래 반환되는 부분에서 생성된 버튼(button 태그)을 클릭했을 때,
> this가 undefined로 나타나는 것에 대해 걱정할 필요가 없다.
>
```js
    handleIncrease() {
        this.setSTate({
            number: this.state.number + 1   
        });
    }

    handleDecrease() {
        this.setSTate({
            number: this.state.number - 1       
        });
    }
``` 
> 이 부분은 화살표함수를 쓰지 않고 함수를 생성했는데 이럴 경우, this가 undefined로 나타나서 제대로 처리되지 않게 된다.
> 이는 함수가 버튼의 클릭이벤트로 전달이 되는 과정에서 'this'와의 연결이 끊겨버리기 때문이다.
>
 * this.setState 에 대해 알아보자.

> state에 있는 값을 바꾸기 위해서는 this.setState를 무조건 거쳐야한다.
> React 에서는 setState 함수가 호출되면 컴포넌트가 리렌더링 되도록 설계되어 있다.
>
 * ... 전개연산자에 대해 알아보자.
 ```js
state = {
    number: 0,
    foo: {
        bar: 0,
        foobar: 1
    }
}
```
> 이런 코드가 있다고 가정했을 때, foo안의 foobar 값을 바꾸고 싶다면
```js
this.setState({
    number: 0,
    foo: {
        ...this.state.foo,
        foobar: 2
    }
})
```
> 이런 식으로 작성을 해 주면, 기존의 객체 안에 있는 내용을 해당 위치에다가 풀어준다.
> 그렇다면 foobar가 2로 바뀌고 기존의 내용도 따라오게 된다.
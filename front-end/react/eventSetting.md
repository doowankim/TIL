* 이벤트 설정

```js
render() {
    return (
        <div>
            <div>값: {this.state.number}</div>
            <button onCLick={this.handleIncrease}>+</button>
            <button onCLick={this.handleDecrease}>-</button>
        </div>
    );
}
```
> 위 코드에서는 버튼이 클릭되면 우리가 준비한 함수(handleIncrease, handleDecrease)가 호출되도록 설정해주었다.

```js
<button onCLick={this.handleIncrease}>+</button>
```
> 여기에서 주의해야 할 점 2가지가 있다.
> * 이벤트 이름을 설정할 때 camelCase로 설정해야 한다. ex) onclick -> onClick, onchange -> onChange
> 
> * 이벤트에 전달해주는 값은 함수여야 한다.
> `onClick={this.handleIncrease()}` 이런식으로 하게 된다면 렌더링을 할 때마다 해당 함수가 호출된다.
> 그렇기 때문에 렌더링 함수에서 이벤트를 설정할 때 본인이 만든 메소드를 호출하면 안된다!!
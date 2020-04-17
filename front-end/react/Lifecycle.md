### 컴포넌트가 브라우저에 나타나기 전, 후에 호출되는 API들이 있다.

* constructor
```js
constructor(props) {
    super(props);
}
```
> 위의 코드는 컴포넌트 생성자 함수이다. 컴포넌트가 새로 만들어질 때마다 constructor가 호출된다.
>
* componentDidMount
```js
componentDidMount() {

}
```
> componentDidMount() 에서는 컴포넌트가 화면에 나타나게 됐을 때 호출된다.
> 여기선 주로 D3, masonry처럼 DOM을 사용해야 하는 `외부 라이브러리 연동`을 하거나
> 해당 컴포넌트에서 필요로 하는 `데이터를 요청`하기 위해 `axios, fetch 등을 통하여 ajax 요청`을 하거나
> DOM의 속성을 읽거나 직접 변경하는 작업을 진행한다.

* componentWillReceiveProps
```js
componentWillReceiveProps(nextProps) {
    /// this.props는 아직 바뀌지 않은 상태
}
```
> componentWillReceiveProps()는 컴포넌트가 새로운 props를 받게 됐을 때 호출된다.
> 이 안에서는 주로 state가 props에 따라 변해야 하는 로직을 작성한다. 
> 새로 받게 될 props는 nextProps로 조회할 수 있으며, 이 때 this.props를 조회하면
> 업데이트 되기 전의 API이니 주의해야 한다.
>
> 그리고 이 기능은 상황에 따라 새로운 API getDerivedStateFromProps()로 대체될 수 있다.

* [New] static getDerivedStateFromProps()
```js
static getDerivedStateFromProps(nextProps, prevState) {
    // 여기서는 setState를 하는 것이 아니라
    // 특정 props가 바뀔 때 설정하고, 설정하고 싶은 state 값을 리턴하는 형태로 사용된다.
    /*
    if (nextProps.value !== prevState.value) {
        return { value: nextProps.value };
    }
    return null; // null을 리턴하면 따로 업데이트 할 것은 없다라는 의미
    */
}
```
> v16.3 이후에 만들어진 getDerivedStateFromProps() API는 props로 받아온 값을
> state로 동기화 하는 작업을 해줘야 하는 경우에 사용된다.


* shouldComponentUpdate
```js
shouldComponentUpdate(nextProps, nextState) {
    // return false 하면 업데이트를 안함
    // return this.props.checked !== nextProps.checked
    return true;
}
```
> shouldComponentUpdate() API는 컴포넌트를 최적화하는 작업에서 매우 유용하게 사용된다.
> 
> 리액트에서는 변화가 발생하는 부분만 업데이트를 해줘서 성능이 꽤 잘 나온다.
> 하지만 변화가 발생한 부분만 감지해내기 위해서는 Virtual DOM에 한번 그려줘야 한다.
> 
> 즉, 현재 컴포넌트의 상태가 업데이트되지 않아도, 부모 컴포넌트가 리렌더링되면, 자식 컴포넌트들도 렌더링된다.
> 여기서 `렌더링` 된다는건, `render() 함수가 호출`된다는 의미이다.
>
> 변화가 없으면 DOM 조작은 하지 않게 된다. 그저 Virtual DOM에만 렌더링 할 뿐이다.
> 이 작업은 그렇게 부하가 많은 작업은 아니지만, 컴포넌트가 무수히 많이 렌더링된다면 얘기가 조금 달라진다.
> CPU 자원을 어느정도 사용하고 있는 것은 사실이기 때문이다.
>
> * 따라서 쓸 데없이 낭비되고 있는 이 CPU 처리량을 줄여주기 위해서 Virtual DOM에 리렌더링 하는것도,
> 불필요할 경우엔 방지하기 위해서 shouldComponentUpdate 를 작성한다.

> 이 함수는 기본적으로 true를 반환한다. 따로 작성을 해주어서 조건에 따라 false를 반환하면 해당 조건에는
> render() 함수를 호출하지 않는다.

* componentWillUpdate
```js
componentWillUpdate(nextProps, nextState) {

}
```
> componentWillUpdate()는 shouldComponentUpdate에서 true를 반환했을 때만 호출된다.
> 만약 false를 반환했었다면 이 함수는 호출되지 않는다.
> 여기선 주로 `애니메이션 효과를 초기화` 하거나, `이벤트 리스너를 없애는 작업`을 한다.
> 이 함수가 호출되고 난 다음에는 render()가 호출된다.
>
> 이 API는 v16.3 이후 deprecate 된다. 기존의 기능은 getSnapshotBeforeUpdate로 대체 될 수 있다.

* [New] getSnapshotBeforeUpdate()
> getSnapshotBeforeUpdate() 가 발생하는 시점은 다음과 같다.
> 1. render()
> 2. getSnapshotBeforeUpdate()
> 3. 실제 DOM에 변화 발생
> 4. componentDidUpdate
>
> 이 API를 통해서 DOM 변화가 일어나기 직전의 DOM 상태를 가져오고, 여기서 리턴하는 값은
> componentDidUpdate의 3번째 파라미터로 받아올 수 있게 된다.
```js
getSnapshotBeforeUpdate(prevProps, prevState) {
    // DOM 업데이트가 일어나기 직전의 시점
    // 새 데이터가 상단에 추가되어도 스크롤바를 유지해보겠다.
    // scrollHeight는 전 후를 비교해서 스크롤 위치를 설정하기 위함이고
    // scrollTop 은 이 기능이 이미 크롬에 구현되어 있는데
    // 이미 구현 되어 있다면 처리하지 않도록 하기 위함이다.
    if (preState.array !== this.state.array) {
        const {
            scrollTop, scrollHeight
        } = this.list;

        // 여기서 반환 하는 값은 componentDidMount에서 snapshot 값으로 받아올 수 있다.
        return {
            scrollTop, scrollHeight
        };  
    }
}

componentDidUpdate(prevProps, prevState, snapshot) {
    if (snapshot) {
        const {scrollTop} = this.list;
        if (scrollTop !== snapshot.scrollTop) return; // 기능이 이미 구현되어있다면 처리하지 않는다.
        const diff = this.list.scrollHeight - snapshot.scrollHeight;
        this.list.scrollTop += diff;
    }
}
```

* componentDidUpdate
```js
componentDidUpdate(prevProps, prevState, snapshot) {
   
}
```
> componentDidUpdate API는 컴포넌트에서 render()를 호출하고 난 다음에 발생하게 된다.
> 이 시점에서는 this.props와 this.state가 바뀌어 있다. 그리고 파라미터를 통해 이전의 값인
> prevProps와 prevState를 조회할 수 있다.
> 그리고 getSnapshotBeforeUpdate에서 반환한 snapshot 값은 세 번째 값을 받아온다.

* componentWillUnmount
```js
componentWillUnmount() {
    // 이벤트, setTimeout, 외부 라이브러리 인스턴스 제거
}
```
> 컴포넌트가 더 이상 필요하지 않게 되면 componentWillUnmount() API가 호출된다.
> 여기서는 주로 등록했었던 이벤트르르 제거하고, 만약에 setTimeout을 걸은 것이 있다면
> clearTimeout을 통하여 제거를 한다.
> 추가적으로 외부 라이브러리를 사용한 것이 있고 해당 라이브러리에 
> dispose 기능이 있다면 여기서 호출하면 된다.
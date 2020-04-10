> 리액트 컴포넌트에서 다루는 데이터는 props와 state로 나뉜다.

> props는 부모 컴포넌트가 자식 컴포넌트에게 주는 값이다.

> 자식 컴포넌트에서는 props를 받아오기만 하고, 받아온 props를 직접 수정할 수는 없다.

```js
import React, { Component } from 'react';

class Test extends Component {
    render() {
        return (
            <div>
                Hello, My name is {this.props.name}!
            </div>
        );
    }
}

export default Test;
```
> 위의 코드를 보면 Test라는 컴포넌트를 만들고 name이라는 props를 <strong>this.</strong> 키워드를 통해 > 조회할 수 있다.

```js
import React, { Component } from 'react';
import Test from './Test';

class App extends Component {
    render() {
        return (
            <Test name="React" />
        );
    }
}

export default App;
```
> 위의 코드를 보면 import를 통하여 Test컴포넌트를 불러오고 렌더링한다.
> props 값을 <strong>name="React"</strong> 라고 태그의 속성을 설정해주는 것 처럼 한다.

> 그렇다면 결과 값은 Hello, My name is React! 가 출력이 될 것이다.
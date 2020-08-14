## Viewport 단위가 뭘까?

CSS의 값으로 지정할 수 있는 단위라고 하면 `px`이나 `%`가 익숙할 것이다. 하지만 반응형 사이트 제작에서 `vh`와 `vw` 등 Viewport 단위는 필수 불가결한 요소이다. 지금부터 Viewport 단위의 기본 사용방법에 대해 알아보자.

CSS에 Viewport 단위가 도입된 지 몇 년이 되었다. 브라우저의 크기가 변경될 때마다 값이 바뀐다는 의미에서 진정한 responsive 단위라고 할 수 있다. Viewport 단위에 대해 들어 본 적이 있지만, 자세한 것은 전혀 모르는 사람들은 이 글에서 배워보고 이해해보도록 하자.

## Viewport 단위 소개

CSS Viewport를 기준으로 한 단위는 `vh, vw, vmin, vmax` 총 4개가 있다.

- Viewport Height (vh) : viewport의 높이에 근거한다. **1vh는 viewport의 높이의 1%와 같다**
- Viewport Width (vw) : viewport의 폭에 근거한다. **1vw는 viewport의 넓이의 1%와 같다**
- Viewport Minimum (vmin) : viewport의 (높이와 너비 중) 작은 쪽의 치수에 기초로한다. **viewport의 높이가 폭보다 작은 경우, 1vmin는 viewport의 높이의 1%에 해당한다. 마찬가지로 viewport의 폭이 높이보다 작은 경우, 1vmin는 viewport의 넓이의 1%와 같다**
- Viewport Maximum (vmax) : viewport의 (높이와 너비 중) 큰 쪽의 치수에 기초로한다. **viewport의 높이가 폭보다 큰 경우, 1vmax는 viewport의 높이의 1%에 해당한다. 마찬가지로 viewport의 폭이 높이보다 큰 경우, 1vmax는 viewport의 넓이의 1%와 같다**

> 그렇다면 Viewport가 다양한 상황에서 어떤 값을 가지고 있는지 알아보자.  
> viewport의 폭이 1200px, 높이가 1000px의 경우 10vw는 120px, 10vh는 100px이된다. 이 viewport는 폭이 높이보다 더 크기 때문에 10vmax는 120px, 10vmin는 100px이 된다  
> 이 장치의 방향이 바뀌어 viewport의 폭이 1000px 높이가 1200px되면 10vh는 120px, 10vw는 100px이된다. 흥미롭게도, 10vmax는 큰 쪽의 viewport의 값에 따라 결정되므로 120px 상태이다. 마찬가지로 10vmin도 100px로 그대로이다.  
> 브라우저 창의 크기를 변경하여 viewport의 넓이를 1000px 높이를 800px하면 10vh는 80px, 10vw는 100px이된다. 마찬가지로 10vmax는 100px, 10vmin은 80px이 된다

이 시점에서는 Viewport 단위는 % 지정 것처럼 보일지도 모른다. 그러나 Viewport 단위와 % 사이에 큰 차이가 있다. % 지정 되어있다면 자식 요소의 폭과 높이는 부모 요소의 폭과 높이에 결정된다. 아래의 코드를 보면서 확인해 보자.

[Viewport 직접 실습해보기 1](https://codesandbox.io/s/priceless-leakey-fez1q?file=/src/Test.js)

위의 예제에서 보이는 바와 같이 첫 번째 예에서 자식 요소의 폭은 부모 요소의 너비의 `80%`로 설정되어 있다. 그런데 두 번째 예제에서는 자식 요소의 폭이 `80vw`로 설정되어 있기 때문에 자식 요소의 폭이 부모 요소보다 넓어지고 있는 것을 확인해 볼 수 있다.

## Viewport 단위는 어떻게 혹은 어떤 부분에서 사용할까?

> Viewport 단위는 viewport의 치수를 기준으로 하기 때문에 요소의 폭, 넓이, 크기를 viewport에 맞게 설정해야 하는 상황에서 매우 편리하다.

예를 들어 보자.

> 풀 스크린의 배경 이미지와 섹션

전체 화면으로 표시되는 요소에 배경 이미지를 설정하는 것이 많다. 제품이나 서비스에 대한 개별 섹션이 화면 가득 표시되도록 Web 사이트를 디자인하고 싶은 경우가 있을 것이다. 그러한 경우에는 각 요소의 폭을 `100%`로 높이를 `100vh`로 설정할 수 있다.

위의 내용을 코드로 옮기면 아래와 같이 된다.

```js
import React from 'react';
import styled from 'styled-components';

const Test = () => {
	return (
		<div>
			<FullScreen />
		</div>
	);
};

const FullScreen = styled.div`
	width: 100%;
	height: 100vh;
	color: white;
	background: url('https://s3-us-west-2.amazonaws.com/s.cdpn.io/123941/vwa.jpg')
		center/cover;
`;

export default Test;
```

위의 예제를 code sandbox에서 실행해보시고, 브라우저의 크기를 늘렸다 줄였다 실험해 보시길 바란다.

※ 이미지 출처 : Pixabay

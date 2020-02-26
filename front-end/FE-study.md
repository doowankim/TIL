### 1. DOM 이란?
* DOM (Document Object Model): DOM은 HTML, XML 문서의 객체 기반 표현방식입니다.

![image](https://user-images.githubusercontent.com/55137934/75303138-33214580-5883-11ea-8e91-55da005e869d.png)

> 그러므로 document를 포함한 html, head, body, title, h1 모두 객체이며, 객체로서 접근 및 컨트롤 할 수 있습니다.
> * HTML (HyperText Markup Language): 웹페이지를 구성하기 위한 마크업 언어
> * XML (eXtensible Markup Language): 여러 방면으로 사용가능한 마크업 언어
>
> DOM API의 예시로는
> 1. document.getElementById(id)
> 2. document.createElement(name)
> 3. element.style.left
> 4. class와 id를 이용한 객체 컨트롤
> 
> 등이 있습니다.
>
### 2. DOM의 브라우저 렌더링 과정

![image (1)](https://user-images.githubusercontent.com/55137934/75303397-f4d85600-5883-11ea-9f7f-84cf1735bf4f.png)

> 1. 브라우저가 html을 전달받게 되면 이것을 바탕으로 DOM 트리를 구성한다.
> 2. DOM 트리는 css와 함께 화면을 그려줄 render 트리를 구성한다.
> 3. layout과 paint를 통해 화면에 보여진다.

### 3. DOM의 문제점

> 1. 브라우저에서 DOM의 변화가 일어나게 되면, 브라우저는 위의 렌더링 과정을 다시 거치는 비효율적인 면이 발생합니다.
> (한 페이지에서 많은 조작이 일어나는 SPA에서는 더더욱 비효율적임)
> 2. DOM의 element를 조작하는 과정에서 쓰였던 기존의 document.getElementById()나 Jquery같은 API가
>프로그램의 규모가 커지면 element의 수도 늘어나고 이벤트도 늘어나기 때문에 api 조작이 불편해집니다.
>
### 4. Virtual DOM
> 이러한 DOM의 문제점을 해결하고자 나온 것이 virtual DOM(가상 DOM)
>
> 핵심원리 : 많은 조작이 일어나고 많은 뷰가 바뀌는 과정을 바로 DOM으로 연산하는 것이 아니라
>가상 DOM을 통해 연산하고 최종 결과를 DOM에 전달!
>
> DOM의 문제점 해결
> 1. 렌더링을 요소가 바뀔 때마다 리렌더링 하는 방식이 아닌 가상 DOM에서 거친 최종결과를 DOM에 전달하는 방식을 통해 효율 증가
> 2. 예를 들어 리액트의 경우 가상DOM과 비슷한 개념인 component를 사용하여 element들의 관리도 쉬워집니다.
## HTML Tag

>html 태그는 모든 HTML 요소의 부모 요소이며 웹페이지에 단 하나만 존재한다. 
>즉, 모든 요소는 html 요소의 자식 요소이며 html 요소 내부에 기술해야 한다. 단 <!DOCTYPE>는 예외이다.
```
<!DOCTYPE HTML>
<html>
  <head>
    <meta charset="utf-8">
    <title>문서 제목</title>
  </head>
  <body>
    화면에 표시할 모든 콘텐츠는 이곳에 기술한다.
  </body>
</html>
```

>html은 글로벌 어트리뷰트를 지원한다.
>특히 lang 어트리뷰트를 사용하는 경우가 많다. 
>다음은 한국어를 주언어로 사용하는 경우의 예이다.
```
<html lang="ko">
```

## script Tag

>script 요소에는 client-side JavaScript를 정의한다.
```js
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <script>
      document.addEventListener('click', function () {
        alert('Clicked!');
      });
    </script>
  </head>
  <body>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
  </body>
</html>
```
>src 어트리뷰트를 사용하면 외부 JavaScript 파일을 로드할 수 있다.
```js
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <script src="main.js"></script>
  </head>
  <body>
    Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
  </body>
</html>
```

## meta Tag
>meta 요소는 description, keywords, author, 기타 메타데이터 정의에 사용된다. 
>메타데이터는 브라우저, 검색엔진(keywords) 등에 의해 사용된다.
>
>charset 어트리뷰트는 브라우저가 사용할 문자셋을 정의한다.
```js
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
  </head>
  <body>
    <p>안녕하세요</p>
    <p>Hello</p>
    <p>こんにちは</p>
    <p>你好</p>
    <p>שלום</p>
    <p>สวัสดี</p>
  </body>
</html>
 ```
>SEO(검색엔진 최적화)를 위해 검색엔진이 사용할 keywords을 정의한다.
```js
<meta name="keywords" content="HTML, CSS, XML, XHTML, JavaScript">
 ```
>웹페이지의 설명을 정의한다.
```js
 <meta name="description" content="Web tutorials on HTML and CSS">
```
>웹페이지의 저자을 명기한다.
```js
 <meta name="author" content="John Doe">
```
>웹페이지를 30초 마다 Refresh한다.
```js
 <meta http-equiv="refresh" content="30">
```

## body Tag
>body tag는 HTML 문서의 내용을 나타내며 웹페이지에 단 하나만 존재한다. 
>메타데이터를 제외한 웹페이지를 구성하는 대부분의 요소가 body 요소 내에 기술된다.
```js
 <html>
   <head>
     <meta charset="utf-8">
     <title>문서 제목</title>
   </head>
   <body>
     Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
   </body>
 </html>
```
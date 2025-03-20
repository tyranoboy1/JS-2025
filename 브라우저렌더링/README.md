## 브라우저 렌더링

> 1. HTML, CSS, 자바스크립트, 이미지, 폰트, 파일 등 렌더링에 필요한 리소스를 요청, 서버로부터 응답을 받는다.
> 2. 렌더링 엔진은 서버로부터 응답된 HTML과 CSS를 파싱하여 DOM과 CSSOM을 생성하고 결합하여 렌더 트리 생성
> 3. 렌더 트리를 기반으로 HTML 요소의 레이아웃을 계산, 브라우저 화면에 HTML 요소 페인팅

## HTML 파싱과 DOM 생성

 ```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="style.css">
</head>
<body>
<ul>
    <li id="apple">Apple</li>
    <li id="banana">Banana</li>
    <li id="orange">Orange</li>
</ul>
<script src="app.js"></script>
</body>
</html>
```
>* 렌더링 엔진은 HTML 문서를 파싱하여 브라우저가 이해할 수 있는 자료구조인 DOM을 생성한다.
>*  ***DOM은 HTML 문서를 파싱한 결과물이다.***


## CSS 파싱과 CSSOM 생성
 ```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="style.css">
    ...
```
 ```css
body {
font-size: 18px;
}

ul {
list-style-type: none;
}
```
>* CSS를 로드하는 link, style 태그를 만나면 DOM 생성 일시 중단
>* link 태그의 href 어트리뷰트에 지정된 CSS 파일을 서버에 요청하여 로드한 CSS 파일이나 style 태그 내의 CSS를 HTML과 동일한 파싱 과정을 거쳐 CSSOM 생성
>  * 파싱과정 : 바이트 -> 문자 -> 토큰 -> 노드 -> CSSOM
>* CSS 파싱 완료 후 DOM 생성 재개

## 렌더 트리 생성

>* 렌더링을 위한 트리구조의 자료구조
>* 서버로부터 응답된 HTML과 CSS를 파싱하여 각각 DOM과 CSSOM을 생성
>* DOM과 CSSOM이 렌더링을 위해 렌더 트리로 결합
>* 브라우저 화면에 렌더링 되지 않는 노드(meta, script..), CSS에 의해 비표시(display: none..) 등의 노드들 포함x
>  * 화면에 렌더링 되는 노드만으로 구성
>* HTML 요소의 레아이웃 계산, 브라우저 화면에 픽셀을 렌더링 하는 페인팅 처리에 입력

## 자바스크립트 파싱과 실행

>* JS 엔진이 파싱 처리
>* JS를 해석하여 AST(추상적 구문 트리)를 생성
>* 인터프리터가 실행할 수 있는 중간 코드인 바이트코드를 생성하여 실행

## 리플로우와 리페인트

>* DOM, CSSOM 을 변경하는 DOM API가 사용된 경우 DOM, CSSOM 변경
>* DOM, CSSOM이 다시 렌더트리로 결합, 변경된 렌더트리를 기반으로 레이아웃과 페인트 과정을 거쳐 브라우저 렌더링하는 과정

## 자바스크립트 파싱에 의한 HTML 파싱 중단

 ```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="style.css">
</head>
<body>
<ul>
    <li id="apple">Apple</li>
    <li id="banana">Banana</li>
    <li id="orange">Orange</li>
</ul>
<script>
    /*
    DOM API인 document.getElementById는 DOM에서 id가 'apple'인 HTML 요소를
    취득한다. 아래 코드가 실행되는 시점에는 id가 'apple'인 HTML 요소의 파싱이 완료되어
    DOM에 포함되어 있기 때문에 정상적으로 동작한다.
    */
    const $apple = document.getElementById('apple');

    // apple 요소의 css color 프로퍼티 값을 변경한다.
    $apple.style.color = 'red';
</script>
</body>
</html>
```
>* JS가 실행된 시점에는 이미 HTML요소 파싱 후 DOM생성 완료 이후 DOM 조작
>* JS가 실행되기 이전에 DOM 생성 완료되어 렌더링되므로 페이지 로딩 시간 단축
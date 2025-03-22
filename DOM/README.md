## DOM

>* ***HTML 문서의 계층적 구조와 정보를 표현하는 것은 물론 노드 객체의 종류, 노드 타입에 따라 필요한 기능을 프로퍼티와 메서드의 집합인 DOM API로 제공***
>* ***DOM API를 통해 HTML의 구조나 내용 또는 스타일 등을 동적으로 조작***

## 요소 노드 취득

### id를 이용한 요소 노드 취득

> * Document.prototype.getElementById
>   * 인수로 전달한 id 어트리뷰트 값을 갖는 하나의 요소 노드를 탐색하여 반환
>   * 반드시 document를 통해 호출

 ```html
<!DOCTYPE html>
<html>
<body>
<ul>
<li id="apple">Apple</li>
<li id="banana">Banana</li>
<li id="orange">Orange</li>
</ul>
<script>
    // id 값이 'banana'인 요소 노드를 탐색하여 반환한다.
    // 두 번째 li 요소가 파싱되어 생성된 요소 노드가 반환된다.
    const $elem = document.getElementById('banana');

    // id 값이 'grape'인 요소 노드를 탐색하여 반환한다. null이 반환된다.
    const $elem = document.getElementById('grape');
    
    // 취득한 요소 노드의 style.color 프로퍼티 값을 변경한다.
    $elem.style.color = 'red';
</script>
</body>
</html>
```

### 태그 이름을 이용한 요소 노드 취득

> * Document.prototype/Element.prototype.getElementsByTagName
>   * 인수로 전달한 태그 이름을 갖는 모든 요소 노드들을 탐색하여 반환한다.

 ```html
<!DOCTYPE html>
<html>
<body>
<ul>
    <li id="apple">Apple</li>
    <li id="banana">Banana</li>
    <li id="orange">Orange</li>
</ul>
<script>
    // 태그 이름이 li인 요소 노드를 모두 탐색하여 반환한다.
    // 탐색된 요소 노드들은 HTMLCollection 객체에 담겨 반환된다.
    // HTMLCollection 객체는 유사 배열 객체이면서 이터러블이다.
    const $elems = document.getElementsByTagName('li');

    // 취득한 모든 요소 노드의 style.color 프로퍼티 값을 변경한다.
    // HTMLCollection 객체를 배열로 변환하여 순회하며 color 프로퍼티 값을 변경한다.
    [...$elems].forEach(elem => { elem.style.color = 'red'; });


    // DOM 전체에서 태그 이름이 li인 요소 노드를 모두 탐색하여 반환한다.
    const $lisFromDocument = document.getElementsByTagName('li');
    console.log($lisFromDocument); // HTMLCollection(4) [li, li, li, li]

    // #fruits 요소의 자손 노드 중에서 태그 이름이 li인 요소 노드를 모두
    // 탐색하여 반환한다.
    const $fruits = document.getElementById('fruits');
    const $lisFromFruits = $fruits.getElementsByTagName('li');
    console.log($lisFromFruits); // HTMLCollection(3) [li, li, li]
</script>
</body>
</html>
```

### class를 이용한 요소 노드 취득

> * Document.prototype/Element.prototype.getElementsByClassName
>   * 인수로 전달한 class 어트리뷰트 값을 갖는 모든 요소 노드들을 탐색하여 반환한다.
>   * 인수로 전달할 class 값은 공백으로 구분하여 여러 개의 class 지정

 ```html
<!DOCTYPE html>
<html>
<body>
<ul>
    <li class="fruit apple">Apple</li>
    <li class="fruit banana">Banana</li>
    <li class="fruit orange">Orange</li>
</ul>
<script>
    // class 값이 'fruit'인 요소 노드를 모두 탐색하여 HTMLCollection 객체에 담아 반환한다.
    const $elems = document.getElementsByClassName('fruit');

    // 취득한 모든 요소의 CSS color 프로퍼티 값을 변경한다.
    [...$elems].forEach(elem => { elem.style.color = 'red'; });

    // class 값이 'fruit apple'인 요소 노드를 모두 탐색하여 HTMLCollection 객체에 담아 반환한다.
    const $apples = document.getElementsByClassName('fruit apple');

    // 취득한 모든 요소 노드의 style.color 프로퍼티 값을 변경한다.
    [...$apples].forEach(elem => { elem.style.color = 'blue'; });
</script>
</body>
</html>
```

### CSS 선택자를 이용한 요소 노드 취득

 ```css
/* 전체 선택자: 모든 요소를 선택 */
* { ... }
/* 태그 선택자: 모든 p 태그 요소를 모두 선택 */
p { ... }
/* id 선택자: id 값이 'foo'인 요소를 모두 선택 */
#foo { ... }
/* class 선택자: class 값이 'foo'인 요소를 모두 선택 */
.foo { ... }
/* 어트리뷰트 선택자: input 요소 중에 type 어트리뷰트 값이 'text'인 요소를 모두 선택 */
input[type=text] { ... }
/* 후손 선택자: div 요소의 후손 요소 중 p 요소를 모두 선택 */
div p { ... }
/* 자식 선택자: div 요소의 자식 요소 중 p 요소를 모두 선택 */
div > p { ... }
/* 인접 형제 선택자: p 요소의 형제 요소 중에 p 요소 바로 뒤에 위치하는 ul 요소를 선택 */
p + ul { ... }
/* 일반 형제 선택자: p 요소의 형제 요소 중에 p 요소 뒤에 위치하는 ul 요소를 모두 선택 */
p ~ ul { ... }
/* 가상 클래스 선택자: hover 상태인 a 요소를 모두 선택 */
a:hover { ... }
/* 가상 요소 선택자: p 요소의 콘텐츠의 앞에 위치하는 공간을 선택
일반적으로 content 프로퍼티와 함께 사용된다. */
p::before { ... }
```

 ```html
<!DOCTYPE html>
<html>
<body>
<ul>
    <li class="apple">Apple</li>
    <li class="banana">Banana</li>
    <li class="orange">Orange</li>
</ul>
<script>
    // class 어트리뷰트 값이 'banana'인 첫 번째 요소 노드를 탐색하여 반환한다.
    const $elem = document.querySelector('.banana');

    // 취득한 요소 노드의 style.color 프로퍼티 값을 변경한다.
    $elem.style.color = 'red';


    // ul 요소의 자식 요소인 li 요소를 모두 탐색하여 반환한다.
    const $elems = document.querySelectorAll('ul > li');
    // 취득한 요소 노드들은 NodeList 객체에 담겨 반환된다.
    console.log($elems); // NodeList(3) [li.apple, li.banana, li.orange]

    // 취득한 모든 요소 노드의 style.color 프로퍼티 값을 변경한다.
    // NodeList는 forEach 메서드를 제공한다.
    $elems.forEach(elem => { elem.style.color = 'red'; });
</script>
</body>
</html>
```

### 특정 요소 노드를 취득할 수 있는지 확인

> * Element.prototype.matches
>   * 인수로 전달한 CSS 선택자를 통해 특정 요소 노드를 취득할 수 있는지 확인
 
```html
<!DOCTYPE html>
<html>
  <body>
    <ul id="fruits">
      <li class="apple">Apple</li>
      <li class="banana">Banana</li>
      <li class="orange">Orange</li>
    </ul>
  </body>
  <script>
    const $apple = document.querySelector('.apple');

    // $apple 노드는 '#fruits > li.apple'로 취득할 수 있다.
    console.log($apple.matches('#fruits > li.apple'));  // true

    // $apple 노드는 '#fruits > li.banana'로 취득할 수 없다.
    console.log($apple.matches('#fruits > li.banana')); // false
  </script>
</html>
```

### HTMLCollection 과 NodeList

> * 여러 개의 결과값을 반환하기 위한 DOM 컬렉션 객체

#### HTMLCollection

getElementsByTagName, getElementsByClassName 메서드가 반환하는 HTMLCollection 객체는<br/>
노드 객체의 상태 변화를 실시간으로 반영하는 살아 있는 DOM 컬렉션 객체

```html
<!DOCTYPE html>
<head>
    <style>
        .red { color: red; }
        .blue { color: blue; }
    </style>
</head>
<html>
<body>
<ul id="fruits">
    <li class="red">Apple</li>
    <li class="red">Banana</li>
    <li class="red">Orange</li>
</ul>
<script>
    // class 값이 'red'인 요소 노드를 모두 탐색하여 HTMLCollection 객체에 담아 반환한다.
    const $elems = document.getElementsByClassName('red');
    // 이 시점에 HTMLCollection 객체에는 3개의 요소 노드가 담겨 있다.
    console.log($elems); // HTMLCollection(3) [li.red, li.red, li.red]

    // HTMLCollection 객체의 모든 요소의 class 값을 'blue'로 변경한다.
    for (let i = 0; i < $elems.length; i++) {
        $elems[i].className = 'blue';
    }
    
    // 실시간 컬렉션이기 때문에 위 방법이 아닌
    // 유사 배열 객체이면서 이터러블인 HTMLCollection을 배열로 변환하여 순회
    [...$elems].forEach(elem => elem.className = 'blue');

    // HTMLCollection 객체의 요소가 3개에서 1개로 변경되었다.
    console.log($elems); // HTMLCollection(1) [li.red]
</script>
</body>
</html>
```

#### NodeList

querySelectorAll 메서드는 실시간으로 노드 객체의 상태 변경을 반영하지 않는 객체인 NodeList 반환

```javascript
// querySelectorAll은 DOM 컬렉션 객체인 NodeList를 반환한다.
const $elems = document.querySelectorAll('.red');

// NodeList 객체는 NodeList.prototype.forEach 메서드를 상속받아 사용할 수 있다.
$elems.forEach(elem => elem.className = 'blue');
```

> * ***childNodes 프로퍼티가 반환하는 NodeList 객체만 HTMLCollection 객체와 같이 실시간으로 노드 객체의 상태 변경을 반영하는 live 객체로 동작***

```html
<!DOCTYPE html>
<html>
<body>
<ul id="fruits">
    <li>Apple</li>
    <li>Banana</li>
</ul>
</body>
<script>
    const $fruits = document.getElementById('fruits');

    // childNodes 프로퍼티는 NodeList 객체(live)를 반환한다.
    const { childNodes } = $fruits;

    // 스프레드 문법을 사용하여 NodeList 객체를 배열로 변환한다.
    [...childNodes].forEach(childNode => {
        $fruits.removeChild(childNode);
    });

    // $fruits 요소의 모든 자식 노드가 모두 삭제되었다.
    console.log(childNodes); // NodeList []
</script>
</html>
```
>*  ***노드 객체의 상태 변경과 상관없이 안전하게 DOM 컬렉션을 사용하려면 HTMLCollection이나 NodeList 객체를 배열로 변환하여 사용하는 것을 권장***


## 노드 탐색

### 자식 노드 탐색

```html
<!DOCTYPE html>
<html>
<body>
<ul id="fruits">
    <li class="apple">Apple</li>
    <li class="banana">Banana</li>
    <li class="orange">Orange</li>
</ul>
</body>
<script>
    // 노드 탐색의 기점이 되는 #fruits 요소 노드를 취득한다.
    const $fruits = document.getElementById('fruits');

    // #fruits 요소의 모든 자식 노드를 탐색한다.
    // childNodes 프로퍼티가 반환한 NodeList에는 요소 노드뿐만 아니라 텍스트 노드도 포함되어 있다.
    console.log($fruits.childNodes);
    // NodeList(7) [text, li.apple, text, li.banana, text, li.orange, text]

    // #fruits 요소의 모든 자식 노드를 탐색한다.
    // children 프로퍼티가 반환한 HTMLCollection에는 요소 노드만 포함되어 있다.
    console.log($fruits.children);
    // HTMLCollection(3) [li.apple, li.banana, li.orange]

    // #fruits 요소의 첫 번째 자식 노드를 탐색한다.
    // firstChild 프로퍼티는 텍스트 노드를 반환할 수도 있다.
    console.log($fruits.firstChild); // #text

    // #fruits 요소의 마지막 자식 노드를 탐색한다.
    // lastChild 프로퍼티는 텍스트 노드를 반환할 수도 있다.
    console.log($fruits.lastChild); // #text

    // #fruits 요소의 첫 번째 자식 노드를 탐색한다.
    // firstElementChild 프로퍼티는 요소 노드만 반환한다.
    console.log($fruits.firstElementChild); // li.apple

    // #fruits 요소의 마지막 자식 노드를 탐색한다.
    // lastElementChild 프로퍼티는 요소 노드만 반환한다.
    console.log($fruits.lastElementChild); // li.orange
</script>
</html>
```

## DOM 조작

### innerHTML

```html
<!DOCTYPE html>
<html>
  <body>
    <ul id="fruits">
      <li class="apple">Apple</li>
    </ul>
  </body>
  <script>
    const $fruits = document.getElementById('fruits');

    // 노드 추가
    $fruits.innerHTML += '<li class="banana">Banana</li>';

    // 노드 교체
    $fruits.innerHTML = '<li class="orange">Orange</li>';

    // 노드 삭제
    $fruits.innerHTML = '';
  </script>
</html>
```

> * 사용자로부터 입력받은 데이터를 그대로 innerHTML 프로퍼티에 할당하는 것은 ***크로스 사이트 스크립팅 공격*** 에 취약하다.


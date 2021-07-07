# DOM 기본

DOM\(Document Object Model\)은 마크업 언어 \(HTML, XML 등\)로 작성된 문서에 액세스하기 위한 표준적인 구조로 Javascript에 한정하지 않고 주로 사용하는 언어 대부분에서도 지원하고 있다. 

클라이언트 측 Javascript로 개발할 때 기본적으로 알아봐야 할 것은 아래와 같다.

* 요소 노드 조작
* 문서 트리간의 왕래
* 이벤트 구동 모델

## 문서 트리와 노드

DOM은 문서를 문서 트리로서 취급한다. DOM에서는 문서에 포함되는 요소나 속성, 텍스트를 각각 객체로 보기 때문에 객체의 집합이 문서라고 생각하면 된다. 문서를 구성하는 요소나 속성, 텍스트 등의 객체를 **노드** 라고 부르며 객체의 종류에 따라 **요소 노드**, **속성 노드**, **텍스트 노드** 등으로 부른다. 각각의 노드는 트리상에서 상하관계에 따라 **루트 노드**, **부모 노드**, **자식 노드**, **형제 노드** 로 불리기도 한다.

```markup
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8"/>
        <title>javascript study</title>
    </head>
    <body>
        <p id="greet">this is <strong>document tree</strong></p>
    </body>
</html>
```

DOM은 이들 노드를 추출, 추가, 변경, 삭제 하기 위한 수단을 제공하는 API라고 할 수 있다.



## 요소 노드 얻기

요소 노드를 얻는 방법은 여러 방법이 있다.

### ID값을 키값으로 노드 얻기 \(getElementById\)

getElementById 메서드는 지정된 ID 값을 갖는 요소를 Element 객체로서 얻는다.

```javascript
document.getElementById(id)
```

```markup
현재시간:<span id="result"></span>
```

```javascript
var current = new Date();
var result = document.getElementById('result');

result.textContent = current.toLocaleString();
```

* 얻은 요소에 텍스트를 삽입하려면 textContent 프로퍼티를 이용한다.



### 태그명을 키값으로 노드 얻기 \(getElementsByTagName\)

태그명으로도 노드를 얻을 수 있다. 대신 id값을 키로 하는 경우와 달리 태그명에서는 해당 태그명을 가지는 여러 요소가 반환된다.  

```javascript
document.getElementsByTagName(tagName)
```

getElementsByTagName 메서드 반환값은 HTMLCollection 객체이며, 해당 객체로부터 이용할 수 있는 멤버는 아래와 같다.

| 멤 | 설명 |
| :--- | :--- |
| length | 리스트에 포함되는 요소  |
| item\(i\) | i번째 노드 |
| namedItem\(name\) | id 또는 name 속성이 일치하는 요소 노드 |

```markup
<ul>
  <li><a href="https://www.google.com">google</a></li>
  <li><a href="https://www.apple.com">apple</a></li>
  <li><a href="https://www.github.com">github</a></li>
</ul>
```

```javascript
var list = document.getElementsByTagName("a")

for(var i = 0, len = list.length; i < len; i++) {
  console.log(list.item(i).href);
}

/*
https://www.google.com/
https://www.apple.com/
https://www.github.com/
*/
```

#### 

### name 속성을 키값으로 노드 얻기 \(getElementsByName\)

name 속성을 키로 요소를 얻는 메서드도 있다. 일반적으로 &lt;input&gt;, &lt;select&gt; 같은 폼 요소에서의 접근에서 이용한다.

```javascript
document.getElementsByName(name)
```



### class 속성을 키값으로 노드 얻기 \(getElementsByClassName\)

해당 메서드를 이용하면 class 속성을 키로하여 HTMLCollection을 얻을 

```javascript
document.getElementsByClassName(className)
```



### 셀렉터 식에 일치하는 요소 얻기 \(querySelector, querySelectorAll\)

셀렉터 식은 css에서 이용되고 있던 표기법으로, 스타일을 적용할 대상을 특정하기 위한 구조이다. 셀렉터 식으로 문서를 검색하여 일치하는 요소를 찾을 수 있다.

```javascript
document.querySelector(selector)
document.querySelectorAll(selector)
```

주로 사용하는 셀렉터 식은 아래와 같다.

| 셀렉 | 설 | 예 |
| :--- | :--- | :--- |
| \* | 모든 요소를 얻는다. | \* |
| \#id | 지정한 id의 요소를 얻는다. | \#main |
| .class | 지정한 클래스이름의 요소를 얻는다. | .external |
| elem | 지정한 태그명의 요소를 얻는다. | li |
| selector1, selector2, ... | 해당하는 셀럭터에 일치하는 요소를 모두 얻는다. | \#main, li |
| parent &gt; child | parent 요소의 자식요소 child를 얻는다. | \#main &gt; div |
| ancestor descendant | ancestor 요소의 자식 요소 descendant를 모두 얻는다. | \#list li |
| prev + next | prev 요소 전후의 next 요소를 얻는다. | \#main + div |
| prev ~ next | prev 요소 이후의 siblings 형제 요소를 얻는다. | \#main ~ div |
| \[attr\] | 지정한 속성을 가진 요소를 얻는다. | input\[type\] |
| \[attr = value\] | 속성이 value값과 같은 요소를 얻는다. | input\[type = "button" |
| \[attr ^= value\] | 속성이 value로 시작하는 값을 가지는 요소를 얻는다. | a\[href^="https://"\] |
| \[attr $= value\] | 속성이 value로 끝나는 값을 가지는 요소를 얻는다. | img\[src$=".gif"\] |
| \[attr \*= value\] | 속성이 value를 포함하는 값을 가지는 요소를 얻는다. | \[title\*="sample"\] |
| \[selector1\] \[selector2\] ... | 복수의 속성 필터에 모두 매치하는 요소를 얻는다. | img\[src\]\[alt\] |



## 노드 워킹

하나의 노드를 기점으로 상대적인 위치 관계에서 노드를 검색할 수도 있다. 트리구조의 노드 사이를 가지를 따라 이동하는 모습 때문에 이를 **노드 워킹** 이라고도 부른다. 노드워킹은 노드의 프로퍼티를 이용한다.

* parentNode: 부모 노드
* previousSibling: 왼쪽 노드
* previousElementSibling: 왼쪽 요소
* nextSibling: 오른쪽 노드
* nextElementSibling: 오른쪽 요소
* firstChild: 처음 자식 노드
* firstElementChild: 처음 자식 요소
* lastChild: 마지막 자식 노드
* lastElementChild: 마지막 자식 요소
* childNodes: 모든 자식 노드

### 노드 워킹 기본

보통, getXxx / queryXxx 메서드로 특정 요소를 얻은 뒤 근접한 노드는 노드워킹으로 얻는다.

```markup
<form>
  <label for="food">food</label>
  <select id="food">
    <option value="ramen">ramen</option>
    <option value="hamburger">hamburger</option>
    <option value="steak">steak</option>
  </select>

  <input type="submit" value="송신"/>
</form>
```

```javascript
var s = document.getElementById('food');

var opts = s.childNodes;

for (var i = 0, len = opts.length; i < len; i++) {
  var opt = opts.item(i);

  if (opt.nodeType === 1) {
    console.log(opt.value);
  }
}
```

* childNodes는 자식 노드를 모두 가져오는데 이 노드는 요소만이 아니기 때문에 nodeType으로 요소인지 체크도 해야 한다.
* nodeType에 대한 정보는 아래와 같다.

| nodeType | 설 |
| :--- | :--- |
| 1 | 요소 노드 |
| 2 | 속성 노드 |
| 3 | 텍스트 노드 |
| 4 | CDATA 섹션 |
| 5 | 실제 참조 노드 |
| 6 | 실제 선언 노드 |
| 7 | 처리 명령 노드 |
| 8 | 주석 노드 |
| 9 | 문서 노드 |
| 10 | 문서형 선언 노드 |
| 11 | 문서의 단편 |
| 12 | 기법 선언 노드 |

### 자식 요소 리스트를 얻는 다른 방법 - firstChild / nextSibling

firstChild /nextSibling 프로퍼티를 이용하여 자식노드를 순회할 수도 있다.

```javascript
var s = document.getElementById('food');

var child = s.firstChild

while(child) {
  if (child.nodeType === 1) {
    console.log(child.value);
  }

  child = child.nextSibling;
}
```

### 자식 요소 리스트를 얻는 다른 방법 - firstElementChild / nextElementSibling

firstElementChild / nextElementSibling은 요소 노드를 리턴하기 때문에 nodeType 체크를 할 필요가 없다.

```javascript
var s = document.getElementById('food');

var child = s.firstElementChild

while(child) {
  console.log(child.value);
  child = child.nextElementSibling;
}
```



## 이벤트 구동 모델

버튼이 클릭되거나 텍스트 박스의 내용이 변경되는 등의 이벤트가 발생함에 따라 실행하는 코드를 작성할 수 있다. 보통 이러한 모델을 **이벤트 드리븐 모델\(이벤트 구동 모델\)** 이라고 한다. 이 때, 이벤트에 대응해 그 처리 내용을 정의하는 코드를 **이벤트 핸들러** 라고 한다.



### 이벤트 핸들러 / 리스너 정의

이벤트 드리븐 모델에서는 어떤 이벤트가 어떤 요소에서 발생했고 어떤 이벤트 핸들러/리스너에 연관시키는지를 정의해야 한다. Javascript에서는 이러한 이벤트를 연결하기 위해 몇 가지 방법을 제공한다.

* 태그 내의 속성으로 선언
* 요소 객체의 프로퍼티로 선언
* addEventListener 메서드를 사용하여 선언



#### 태그 내의 속성으로 선언

태그 내의 속성으로 메서드를 선언할 수 있다.

```markup
<input type="button" value="다이얼로그 표시" onClick="btn_click()"/>
```

```javascript
function btn_click() {
    window.alert("버튼 클릭");
}
```

메서드 구현이 간단한 경우 속성에 직접 메서드를 기술할 수도 있다.

```markup
<input type="button" value="다이얼로그 표시" onClick="window.alert('버튼 클릭')"/>
```



#### 요소 객체의 프로퍼티로 선언

보통 페이지 구성\(HTML\)과 처리\(Javascript\)는 분리해서 관리하는 것이 좋다. 그래서 javascript 코드에서 요소를 불러와 프로퍼티를 설정하여 이벤트 핸들러 / 리스너를 연결시킬 수 있다.

```markup
<input type="button" value="다이얼로그 표시" onClick="btn_click()"/>
```

```javascript
window.onload = function() {
    document.getElementById('btn').onclick = function() {
        window.alert("버튼 클릭");
    };
};
```

* window.onload 는 페이지 로드 시에 실행되는 이벤트 리스너이다.
* 여기서는 버튼을 불러와 버튼 클릭시 실행되는 이벤트 핸들러를 등록한다.



#### addEventListener 메서드로 선언

요소 객체의 프로퍼티로 선언할 시 문제점은 동일한 요소/동일한 이벤트에 여러 핸들러를 연결시킬 수가 없다는 것이다. \(하나의 메서드는 하나의 기능이 원칙이지만, 여러 이벤트가 발생해야 할 때 요소 객체의 프로퍼티로 선언한다면 하나의 메서드에서 여러 개의 이벤트 로직을 우겨넣어야 한다.\)

대신, addEventListener 메서드로 선언하면 여러 핸들러를 연결시킬 수 있다. addEventListener 메서드의 구조는 다음과 같다.

```javascript
elem.addEventListener(type, listener, capture)
/*
 * type: 이벤트 종류
 * listener: 이벤트에 따라 수행할 작업
 * capture: 이벤트의 방향
 */
```

```markup
<input id="btn" type="button" value="다이얼로그 표시"/>
```

```javascript
document.addEventListener('DOMContentLoaded', function() {
    document.getElementById('btn').addEventListener('click', function() {
        window.alert('버튼 클릭');
    }, false);
}, false);
```

* DOMContentLoaded 이벤트 리스너는 onload 이벤트 핸들러와 마찬가지로 페이지가 로드된 타이밍에 이벤트 처리를 수행한다. 
* 대신 onload는 콘텐츠 본체와 이미지가 로드된 후에 실행하지만 DOMContentLoaded는 콘텐츠 본체가 로드된 후에 실행된다. \(이미지 로드를 기다리지 않는다.\)
* 그래서 DOMContentLoaded가 스크립트 시작 타이밍을 앞당길 수 있기 때문에 이 리스너를 사용하는 것이 맞다.


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



### 요소 노드 얻기

요소 노드를 얻는 방법은 여러 방법이 있다.

#### ID값을 키값으로 노드 얻기 \(getElementById\)

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



#### 태그명을 키값으로 노드 얻기 \(getElementsByTagName\)

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

#### name 속성을 키값으로 노드 얻기 \(getElementsByName\)

name 속성을 키로 요소를 얻는 메서드도 있다. 일반적으로 &lt;input&gt;, &lt;select&gt; 같은 폼 요소에서의 접근에서 이용한다.

```javascript
document.getElementsByName(name)
```



#### class 속성을 키값으로 노드 얻기 \(getElementsByClassName\)

해당 메서드를 이용하면 class 속성을 키로하여 HTMLCollection을 얻을 

```javascript
document.getElementsByClassName(className)
```



#### 셀렉터 식에 일치하는 요소 얻기 \(querySelector, querySelectorAll\)

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




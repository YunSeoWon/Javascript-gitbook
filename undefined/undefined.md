# 변수와 상수, 자료형

### 변수 선언하기 - var

변수 선언은 var 키워드를 사용한다. 여러 개의 변수를 콤마로 구분하여 같이 선언할 수도 있다.

```javascript
var variable // = undefined
var num = 1
var x, y
```

초깃값을 설정하지 않았을 경우에는 undefined를 변수에 할당한다.



### 변수 선언하기 - let

ES2015에는 변수를 선언하는 방식으로 let이 추가되었다.

```javascript
let variable
let num = 1
let x, y
```

#### var와 let의 차이

다음의 특징으로부터 ES2015를 이용할 수 있는 환경에서는 let을 우선으로 사용하자.

1. let은 변수의 중복을 허용하지 않는다. 대신 var는 변수의 중복을 허용한다.

   ```javascript
   let msg = 'hello'
   let msg = 'world'
   // Identifier 'msg' has aleady been declared
   ```

2. let은 블록 스코프를 인식한다. let이 더 세세하게 변수의 유효범위를 관리할 수 있다.

### 상수 선언하기 - const

const 키워드로 상수를 선언할 수 있다.

```javascript
const TAX = 1.00
```



### 명명법

| 대상 | 기 | example |
| :--- | :--- | :--- |
| 변수명 / 함수 | camelCase  | variableName |
| 상수 | under\_score | CONST\_NAME  |
| 클래스 | Pascal | ClassName |

### 자료형

#### 기본

| 데이터 | 개 |
| :--- | :--- |
| 숫자형\(number\) | 숫자 \(0, 1.324, -22.113 등등\) |
| 문자열형\(string\) | 'aa', "aaa"  |
| 논리형\(boolean\) | true / false |
| 심벌형\(symbol\) | 심 |
| 특수형\(null / undefined\) | null / undefined |

#### 참조형

| 데이터 | 개요 |
| :--- | :--- |
| 배열\(array\) | \[1, 2, 3\] |
| 객체\(object\) | { "name": "beer1", "age": 27 } |
| 함수\(function\) | function func\(args\) { ... } |




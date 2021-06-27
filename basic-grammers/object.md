# 객체

## 객체

객체는 객체의 상태나 특성을 나타내기 위한 정보를 의미하는 **프로퍼티**와 객체를 조작하기 위한 기능을 나타내는 **메서드**로 구성된다.

### 객체 생성

객체의 복제를 만드는 것을 **인스턴스화**라고 하고 인스턴스화에 의해 만들어진 복제본을 **인스턴스**라고 부른다. 객체를 인스턴스화 하기 위해서 new 연산자를 이용한다. \(이를 생성자라고 한다.\) 그리고 생성된 변수를 **인스턴스 변수**라고 부른다.

```javascript
var 변수명 = new 객체명([..])
```

인스턴스 변수에서 프로퍼티/메서드를 호출하려면 .\(닷\) 연산자를 사용하면 된다.

```javascript
obj.property ( = value)
obj.method(p1, p2, ...)
```

### 정적 프로퍼티 / 정적 메서드

인스턴스를 생성하지 않고 바로 이용 가능한 프로퍼티/메서드가 있는데 이를 정적 프로퍼티 / 정적 메서드라고 한다.

```javascript
Class.property ( = value)
Class.method(p1, p2, ...)
```

### 내장형 객체

내장형 객체는 javascript에 미리 내장되어 있는 객체이다. 특정 브라우저 환경에서만 돌아가는 객체가 있는데, 내장형 객체는 javascript가 동작하는 모든 환경에서 이용할 수 있는 특징이 있다.

| 객체 | 개 |
| :--- | :--- |
| \(Global\) | Javascript의 기본 기능에 접근하기 위한 수단 제 |
| Object | 모든 객체의 모형이 되는 기능 제공 |
| Array | 배열을 조작하기 위한 기능 제공 |
| MAP/WeakMAP | 키/값으로 이루어진 연상 배열을 조작하기 위한 기능 제공 |
| Set/WeakSet | 고유한 값의 집합을 관리하기 위한 기능 제공 |
| String | 문자열을 조작하기 위한 기능 제공 |
| Boolean | 참/거짓 값을 조작하기 위한 기능 제공 |
| Number | 숫자를 조작하기 위한 기능 제공 |
| Function | 함수를 조작하기 위한 기능 제공 |
| Symbol | 심벌을 조작하기 위한 기능 제공 |
| Math | 수치 연산을 실행하기 위한 기능 제공 |
| Date | 날짜를 조작하기 위한 기능 제 |
| RegExp | 정규식 표현에 관한 기능 제공 |
| Error | 에러 정보를 관리한다. |
| Proxy | 객체의 동작을 커스터마이즈하는 기능 제공 |
| Promise | 비동기 처리를 구현하기 위한 기능 제공 |

```javascript
var str = '안녕하세요'
console.log(str.length) // String의 프로퍼티인 length
```

* length는 String의 프로퍼티인데 Javascript에서는 리터럴 그대로 대응하는 내장형 객체로 이용할 수 있어서 인스턴스화를 의식할 필요가 없다.
* 기본 데이터형에는 new 연산자를 사용하지 않는다. \(String, Boolean, Number, Symbol, Function?\)

기능이 필요할 때 마다 찾아서 쓰자. \(기록해두면 더 좋고..\)

## Global 객체 사용하기

Global 객체는 글로벌 변수나 글로벌 함수를 관리하기 위해 javascript가 자동으로 생성하는 객체이다. Global 객체는 여러가지 특징이 있다.

* 인스턴스화 하는 것이 불가능하다.
* 메서드를 호출할 수 없다.
* Global.xxx가 아닌 xxx를 바로 호출할 수 있다.

글로벌 변수/함수란 어딘가의 밑에 속하지 않은 최상위 변수/함수를 말한다.

Javascript에서 이용 가능한 글로벌 변수/함수는 아래와 같다.

**특수값/체크**

| 멤버 | 개 |
| :--- | :--- |
| NaN | 숫자가 아니다 |
| Infinity | 무한대 |
| undefined | 미정의값 |
| isFinite\(num\) | 유한값인지 아닌지\(NaN, +-Infinity\) 판별  |
| isNaN\(num\) | 숫자가 아닌지 판별 |

**변환**

| 멤버 | 개 |
| :--- | :--- |
| Boolean\(val\) | 논리형으로 변환 |
| Number\(val\) | 숫자형으로 변환 |
| String\(val\) | 문자열로 변환 |
| parseFloat\(str\) | 문자열을 부동소수점 수치로 변환 |
| parseInt\(str\) | 문자열을 정수값으로 변환 |

**인코드/해석**

| 멤버 | 개요 |
| :--- | :--- |
| encodeURI\(str\) | 문자열을 URI 인코딩 |
| decodeURI\(str\) | 문자열을 URI 디코딩 |
| encodeURIComponent\(str\) | 문자열을 URI 인코딩 |
| decodeURIComponent\(str\) | 문자열을 URI 디코딩 |
| eval\(exp\) | 식/값을 계 |


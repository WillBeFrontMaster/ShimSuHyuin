# JavaScript

### JavaScript :

정적인 HTML을 동적으로 표현하기 위해 경량의 프로그래밍 언어 도입 → 자바스크립트 탄생

- HTML, CSS 와 함께 웹을 구성하는 요소 중 하나
- 웹 브라우저에서 동작하는 유일한 프로그래밍 언어
- 별도의 컴파일 작업을 수행하지 않는 인터프리터 언어 (소스코드를 즉시 실행하고 컴파일러는 빠르게 동작하는 머신 코드를 생성하고 최적화)
- 명령형, 함수형, 프로토타입 기반 객체지향 프로그래밍을 지원하는 멀티 패러다임 프로그래밍 언어

### 데이터 타입

1. 원시타입
    - `number`, `string`, `boolean`, `null`, `undefined`, `symbol`(ES6)
2. *객체타입 (원시 타입을 제외한 나머지 값들 - 함수, 배열, 정규표현식 등)
    - `object`

→ 변수 선언 시 데이터 타입을 지정하지 않음. 모든 변수는 var로 선언

* 자바스크립트 객체는 key, value로 구성된  property의 집합. property의 값으로 자바스크립트에서 사용할 수 있는 모든 값을 사용할 수 있다.

* property의 값으로 함수를 사용할 수 있으며, 일반 함수와 구분하기 위해 메소드라 부른다.

## 원시타입

: 변경 불가능한 값이며 값에 의한 전달(pass-by-value)이다.

- number :
    - 특정 숫자 타입이 존재하지 않으며, 모든 수를 실수로 처리한다.
    - `Infinity` : 양의 무한대
    - `-Infinity` : 음의 무한대
    - `NaN` : 산술 연산 불가 (Not A Number)
- string :
    - 텍스트 데이터를 나타내는 데 사용한다.
    - 작은 따옴표(’’) 또는 큰 따옴표(””) 안에 텍스트를 넣어 생성한다.
    
    ```jsx
    var str = 'Hello'; // str은 메모리에 생성된 문자열 'Hello'의 메모리 주소를 가리킴
    str = 'world'; //새로운 문자열 'world' 를 생성하고 가리킴.
    
    //'Hello'와 'world' 모두 메모리에 존재. 가리키는 값이 변경된 것
    ```
    
    - 배열처럼 인덱스를 통해 접근할 수 있다.
    - 이미 생성된 문자열의 일부 문자를 변경하면 반영되지 않지만, 새로운 문자열을 재할당하는 것은 가능하다. (기존 문자열을 변경하는 것이 아니라 새로운 문자열을 새롭게 할당하는 것.)
    
    ```jsx
    var str = 'hello';
    console.log(str); // hello
    
    //문자열을 변경할 수 없다.
    str[0] = 'H';
    console.log(str); // hello
    
    str = 'world';
    console.log(str); // world
    
    str += 'best';
    console.log(str); // world best
    
    str = str.subString(0, 3);
    console.log(str); // wor
    
    str = str.toUpperCase();
    console.log(str); // WOR
    ```
    
- boolean :
    - 논리적 참 거짓을 나타내는 `true`, `false`
    - 비어있는 문자열, `null`, `undefined`, 숫자 0 은 `false`로 간주된다.
- undefined :
    - `undefined` : 선언 이후 값을 할당하지 않는 변수
    - 개발자가 의도적으로 할당한 값이 아니라 자바스크립트 엔진에 의해 초기화 된 값이다.
- null :
    - 변수의 값이 없다는 것을 명시하고 싶은 경우 사용한다.
    - 함수가 호출되었으나 유효한 값을 반환할 수 없는 경우, 명시적으로 null을 반환하기도 한다.
    - `null`은 Null, NULL 등과 다르다.
- symbol :
    - 이름의 충돌 위험이 없는 유일한 객체의 프로퍼티 키를 만들기 위해 사용
    - Symbol 함수를 호출해 생성한다. 이 때 생성된 심볼 값은 다른 심볼 값들과 다른 유일한 심볼 값이다.
    
    ```jsx
    var key = Symbol('key'); // 이름의 충돌 위험이 없는 유일한 객체의 프로퍼티 키
    console.log(typeof key); // symbol
    
    var obj = {};
    obj[key] = 'value';
    console.log(obj[key]); //value
    ```
    

## 객체타입

- object

---

### 변수 :

변수는 한 번 쓰고 버리는 값이 아닌 일정 기간 유지할 필요가 있는 값에 사용한다.

또한, 변수를 사용하면 값의 의미가 명확해져 코드의 가독성이 좋아진다.

변수명은 변수의 존재 목적을 쉽게 이해할 수 있도록 의미있게 지정하여야 한다.

- 변수명의 명명 규칙
    - 반드시 영문자, _, 또는 $로 시작하여야 한다. 이어지는 문자에는 숫자도 사용할 수 있다.
    - 자바스크립트는 대소문자를 구별한다. (radius ≠ Radius)

값을 할당하지 않은 변수는 `undefined`로 초기값을 갖는다. 선언하지 않은 변수에 접근하면 참조오류가 발생한다.

var 키워드로 선언한 변수는 중복 선언이 가능하다. 중복 선언한 변수는 이전 변수의 값을 덮어쓴다.

```jsx
var x = 1;
console.log(x); // 1

var x = 100;
console.log(x); // 100
```

### 동적 타이핑 :

자바스크립트는 동적타입(dynamic/weak type)언어이다. 변수의 타입 지정없이 값이 할당되는 과정에서 타입에 의해 자동으로 타입이 결정된다. 따라서 같은 변수에 여러 타입(undefined, object, number, …)의 값을 할당할 수 있다.

### 변수 호이스팅 :

```jsx
console.log(foo); // 1. undefined

var foo = 'foo';
console.log(foo); // 2. foo
{
	var foo = 'bar';
}
console.log(foo); // 3. bar
```

1 에서 변수 foo 는 아직 선언되지 않았으므로 ‘ReferenceError : foo is not defined’ 가 발생할 것을 기대했지만 콘솔에는 undefined 가 출력된다.

자바스크립트의 특징인, 모든 선언문은 호이스팅(Hoisting)되기 때문이다.

<aside>
💡 호이스팅(Hoisting) 이란?
자바스크립트의 모든 선언문이 해당 Scope의 선두로 옮겨진 것처럼 동작하는 특성을 말한다.
즉, 자바스크립트는 모든 선언문(var, let, const, function, function*, class)이 선언되기 이전에 참조 가능하다.

</aside>

- 호이스팅의 상세 과정 :
    
    변수는 3단계에 걸쳐서 생성된다.
    
    1. 선언 단계(Declaration phase) :  변수 객체(Variable Object)에 변수를 등록한다. 이 변수 객체는 [scope](JavaScript/scope.md)가 참조하는 대상이 된다.
    2. 초기화 단계(Initialization phase) : 변수 객체에 등록된 변수를 메모리에 할당한다. 이 단계에서 변수는 undefined로 초기화된다.
    3. 할당 단계(Assignment phase) : undefined로 초기화된 변수에 실제 값을 할당한다.
    
    이 때 var 키워드로 선언된 변수는 선언 단계와 초기화 단계가 한 번에 이루어진다. 즉, scope에 변수가 등록되고 변수는 메모리에 공간을 확보한 후 undefined로 초기화된다. 따라서 변수 선언문 이전에 변수에 접근하려도 변수 객체에 변수가 존재하기 때문에 에러가 발생하지 않고, undefined를 반환한다. 이러한 현상을 ***변수 호이스팅 (Variable Hoisting)*** 이라 한다.
    
    이후 변수 할당문에 도달하면 비로소 값의 할당이 이루어진다.
    
    위의 예제를 변수 호이스팅 관점에서 다시 한 번 보면,
    
    1 이 실행되기 이전에 `var foo = ‘foo’;` 이 호이스팅되어 1 구문 앞에 `var foo;`가 옮겨진다. (실제로 변수 선언이 코드 레벨로 옮겨진 것은 아니고 변수 객체에 등록되고 undefined로 초기화된 것이다.) 하지만 변수 선언 단계, 초기화 단계가 할당 단계와 분리되어 진행되기 때문에 이 단계에서 foo에 undefined가 할당되어 있다. 변수 foo에 값이 할당되는 것은 2행에서 실시된다.
    2 에서는 변수에 값이 할당되었기 때문에 ‘foo’ 가 출력된다.
자바스크립트의 변수는 블록 레벨 스코프(block-level scope)를 가지지 않고 함수 레벨 스코프(function-level scope)를 갖는다.
단, ES6에서 도입된 let, const키워드를 사용하면 블록 레벨 스코프를 사용할 수 있다.

함수 레벨 스코프(function-level-scope):
	함수 내에서 선언된 변수는 함수 내에서만 유효하며 함수 외부에서는 참조할 수 없다. 즉, 함수 내부에서 선언한 변수는 지역 변수이며 함수 외	부에서 선언한 변수는 모두 전역 변수이다.
블록 레벨 스코프(block-level-scope):
	코드 블록 내에서 선언된 변수는 코드 블록 내에서만 유효하며 코드 블록 외부에서는 참조할 수 없다.


따라서 코드 블록 내의 변수 foo는 전역변수이므로 전역에 선언된 변수 foo에 할당된 값을 재할당하기 때문에 3 의 결과는 ‘bar’이 된다.
    

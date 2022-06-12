Scope
=====

## 스코프(Scope) :
* 스코프(scope, 유효범위)는 참조 대상 식별자(identifier, 변수, 함수의 이름 등 어떤 대상이 다른 대상과 식별되는 유일한 이름)를 찾아내기 위한 규칙이다.   자바스크립트는 이 규칙대로 식별자를 찾는다.   
* 이름이 같은 변수가 전역, 함수 내에서 중복으로 선언되었다면 전역에 선언된 변수는 어디에서든 참조할 수 있고, 함수 내에서 선언된 변수는 함수 내에서만 참조할 수 있다.

```javascript
  var x = 'global'; // 전역 변수 x
  
  function foo (){
    var x = 'function scope'; // 지역 변수 x
    console.log(x);
   }
   
   foo(); // function scope
   console.log(x); // global
```
만약 스코프가 없다면 같은 식별자 이름은 충돌을 일으키므로 프로그래 전체에서 한 번 밖에 사용할 수 없다. (디렉터리가 없는 컴퓨터는 같은 이름을 갖는 파일을 생성할 수 없다.)   
스코프도 이와 같이 식별자 이름의 충돌을 방지한다.   
   
   
## 스코프의 구분
1. 전역 스코프 (Global scope) :   
  코드 어디에서든 참조할 수 있다.
2. 지역 스코프 (Local scope / Fuction-level scope) :   
  함수 코드 블록이 만든 스코프로 함수 자신과 하위 함수에서만 참조할 수 있다.

-> 변수는 선언 위치에 의해 스코프를 가지게 된다. 즉, 전역에서 선언된 변수는 전역 스코프를 갖는 전역 변수이고, 지역에서 선언된 변수는 지역 스코프를 갖는 지역 변수가 된다.   
  전역 스코프를 갖는 전역 변수는 전역에서 참조할 수 있다. 지역에서 선언된 지역 변수는 그 지역과 그 지역의 하부 지역에서만 참조할 수 있다.   

## 스코프의 특징  
* 자바스크립트는 함수 레벨 스코프(Function-level scope)를 따른다 : 
  * 함수 레벨 스코프란, 함수 코드 블록 내에서 선언된 변수는 함수 코드 블록 내에서만 유효하고 함수 외부에서는 유효하지 않다는 것이다.
  * ES6에서 도입된 `let` keyword를 사용하면 블록 레벨 스코프를 사용할 수 있다.

```javascript
  var x = 0;
  {
    var x = 1;
    console.log(x); // 1
  }
  console.log(x); // 1 어라라가 아니고 아하
  
  let y = 0; // in ES6
  {
    let y = 1;
    console.log(y); // 1
  }
  console.log(y); // 0
```


---------------------------<br/><br/>
## 전역 스코프 (Global Scope)
전역에 변수를 선언하면 이 변수는 어디에서든 참조할 수 있는 전역 스코프를 갖는 전역 변수가 된다.   
var 키워드로 선언한 전역 변수는 전역 객체(Global Object) `window` 의 property이다.   
```javascript
  var global = 'global';
  
  function foo(){
    var local = 'local';
    console.log(global); 
    console.log(local); 
  }
  foo(); // global
         // local
  
  console.log(global);
  console.log(local); // Uncaught ReferenceError : local is not defined
```    
변수 global은 전역에서 선언되었다. 자바스크립트는 타 언어와는 달리 특별한 시작점이 없어서 위 코드와 같이 전역에 변수나 함수를 선언하기 쉽다.   
특별한 시작점이 없으므로 코드가 나타나는 즉시 해석되고 실행된다.   
따라서 전역에 변수를 선언하기 쉬우며 이것은 전역 변수를 남발하게 하는 문제를 일으킨다.   
전역 변수의 사용은 변수 이름이 중복될 수 있고, 의도치 않은 재할당에 의한 상태 변화로 코드를 예측하기 어렵게 만드므로 남용을 자제해야 한다.<br/><br/>

## 비 블록 레벨 스코프 (Non block-level scope)   
자바스크립트는 블록 레벨 스코프를 사용하지 않으므로 __함수__ 밖에서 선언된 변수는 코드 블록 내에 선언되었다 하더라도 모두 전역 스코프를 갖게된다.<br/><br/>

## 함수 레벨 스코프 (Function-level scope)   
자바스크립트는 함수 레벨 스코프르 사용한다. 즉, 함수 내에서 선언된 매개변수와 변수는 함수 외부에서는 유효하지 않다.
```js
  var x = 10; // 전역변수
  
  (function(){
    var y = 20; // 지역변수
   })();
   
   console.log(x); // 10
   console.log(y); // 'y' is not defined
```
따라서 변수 y는 지역변수이다.<br/><br/>

```js
  var a = 'global' // 전역변수
  
  function foo(){
    var a = 'local' // 지역변수
    console.log(a);
  }
  
  foo();  // local
  console.log(a); // global
``` 

변수 a가 전역변수, 지역변수로 중복 선언되었다. 전역에서는 전역변수만이 참조 가능하고, 함수 내 지정 영역에서는 전역, 지역 변수 모두 참조 가능하나    
변수명이 중복된 경우 지역변수를 우선하여 참조한다.<br/><br/>

```js
  var x = 'global';
  
  function foo(){
    var x = 'local';
    console.log(x);
    
    function bar(){ // 내부함수
      console.log(x);
    }
    
    bar();
  }
  foo(); // local
         // local
  console.log(x); // global
```
내부함수는 자신을 포함하고 있는 외부함수의 변수에 접근할 수 있다. [클로저](Closuere.md)에서와 같이 내부함수가 더 오래 생존하는 경우, 타 언어와는 다른 움직임을 보인다.<br/>
함수 bar 에서 참조하는 변수 x는 함수 foo 에서 선언된 지역변수이다.<br/>
이는 [실행 컨텍스트](ExecutionContext.md)의 스코프 체인에 의해 참조 순위에서 전역변수 x가 뒤로 밀렸기 때문이다.<br/><br/>

```js
  var x = 10;
  
  function foo(){
    x = 100;
    console.log(x);
  }
  foo(); // 100
  console.log(x); // 100
```
함수 영역에서 전역변수를 참조할 수 있으므로 전역변수의 값도 변경할 수 있다.<br/>
내부 함수의 경우, 전역변수는 물론 상위 함수에서 선언한 변수에 접근/변경이 가능하다.<br/><br/>

```js
  var x = 10;
  
  function foo(){
    var x = 100;
    console.log(x);
    
    function bar(){ // 내부함수
      x = 1000;
      console.log(x);
    }
    
    bar();
  }
  foo();  // 100 1000
  console.log(x); // 1000
```
중첩 스코프는 가장 인접한 지역을 우선하여 참조한다.<br/><br/>

```js
  var foo = function(){
    var a = 3, b = 5;
    
    var bar = function(){
      var b = 7, c = 11;    // a == 3, b == 7, c == 11
      
      a += b + c;   // a == 21, b == 7, c == 11
      
    };
    // a == 3, b == 5, c == undefined
    
    bar();  // a == 21, b == 5
    
    };
```
<br/><br/>
## 렉시컬 스코프
```js
  var x = 1;
  
  function foo(){
    var x = 10;
    bar();
  }
  
  function bar(){
    console.log(x);
  }
  
  foo(); // 1
  bar(); // 1
```
위 예제의 실행 결과는 함수 bar의 상위 스코프가 무엇인지에 따라 결정된다.<br/>
1. 함수를 어디서 __호출__ 했는가 -- 동적 스코프(Dynamic Scope)
2. 함수를 어디서 __선언__ 했는가 -- 렉시컬 스코프(Lexical Scope) 또는 정적 스코프(Static Scope)

첫 번째 방식으로 함수의 상위 스코프를 결정한다면 함수 bar의 상위 스코프는 함수 foo의 전역일 것이고(foo에서 호출), 두 번째 방식으로 함수의 스코프를 결정한다면 함수 bar의 스코프는 전역일 것이다(전역에서 선언).<br/>
자바스크립트를 비롯한 대부분의 프로그래밍 언어는 렉시컬 스코프를 따르는데, __렉시컬 스코프는 함수를 어디에 선언하였는지에 따라 결정된다.__ <br/>자바스크립트는 렉시컬 스코프를 따르므로 함수를 선언한 시점에 상위 스코프가 결정된다. 함수를 어디에서 호출하였는지는 스코프 결정에 아무 의미도 주지 않는다.<br/>
위 예제의 함수 bar는 전역에 선언되었다. 따라서 함수 bar의 상위 스코프는 전역 스코프이고 전역 변수 x의 값 1을 두 번 출력한다.<br/><br/>

## 암묵적 전역
```js
  var x = 10; 
  
  function foo(){
    y = 20; // 선언하지 않은 식별자
    console.log(x+y);
  }
  
  foo();  // 30
```
위 예제의 y는 선언하지 않은 식별자이다. 따라서 y = 20 이 실행되면 참조 에러가 발생할 것 같지만, 선언하지 않은 식별자 y는 마치 선언된 변수처럼 동작한다. 이는 선언하지 않은 식별자에 값을 할당하면 __전역 객체의 프로퍼티__ 가 되기 때문이다.<br/>
<br/>
함수 foo가 호출되면 자바스크립트 엔진은 변수 y에 값을 할당하기 위해 먼저 스코프 체인을 통해 선언된 변수인지 확인한다. 이 때, 함수 foo의 스코프와 전역 스코프 어디에서도 변수 y의 선언을 찾을 수 없으므로 참조 오류가 발생해야 하지만 자바스크립트 엔진은 `y = 20` 을 `window.y = 20` 으로 해석하여 프로퍼티를 동적 생성한다. 그 결과 y느 전역 객체의 프로퍼티가 되어 마치 전역 변수처럼 동작한다.<br/>
이러한 현상을 __암묵적 전역(implict global)__ 이라 한다.
<br/><br/>
하지만 y는 변수 선언없이 단지 전역 객체의 프로퍼티로 추가되었을 뿐이지 변수가 아니다. 따라서 변수가 아닌 y는 변수 호이스팅이 발생하지 않는다.<br/>
<br/>
변수가 아니라 단지 프로퍼티인 y는 delete 연산자로 삭제할 수 있다. 전역 변수느 프로퍼티이지만 delete 연산자로 삭제할 수 없디.<br/>

```js
  var x = 10;
  
  function foo(){
    y = 20; // 선언하지 않은 변수
    console.log(x + y);
  }
  
  foo(); // 30
  
  console.log(window.x); // 10
  console.log(window.y); // 20
  
  delete x;
  delete y;
  
  console.log(window.x); // 10 전역 변수느 삭제되지 않는다.
  console.log(window.y); // undefined 프로퍼티는 삭제된다.
```
<br/>
<br/>

### 최소한의 전역변수 사용<br/>
1. 애플리케이션에서 전역변수 사용을 위해 전역변수객체를 만들어 사용한다.
2. 즉시실행함수(즉시 실행되고 전역에서 바로 사라진다)를 사용한다.

  
  
  
  
  

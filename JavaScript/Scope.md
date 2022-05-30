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


---------------------------   
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
전역 변수의 사용은 변수 이름이 중복될 수 있고, 의도치 않은 재할당에 의한 상태 변화로 코드를 예측하기 어렵게 만드므로 남용을 자제해야 한다. 


  
  
  
  
  
  
  
  
  
  
  
  
  
  
  

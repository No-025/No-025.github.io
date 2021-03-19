---
title: "210318-자바스크립트"
toc: tru
toc_label: "자바스크립트"
categories:
  - Javascript
---
# 자바스트립트 문법

## 자바스트립트 변수

`var, let, const`로 선언



## 자바스크립트의 비교연산자

==보다 타입까지 비교하는 `===`를 사용한다.(**권장**) 

```
0 =="0"		true
0 === "0"	false
```


## 자바스크립트의 Type

타입은 선언할 때가 아니라, `실행타임`에 결정됨

*`toString.call()`: 자바스트립트 타입 확인


---

> [자바스크립트 기본문법 참고](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide)

---

# 자바스크립트 함수


## 호이스팅(Hoisting)

함수 안에 있는 선언들을 모두 끌어 올려서 해당 함수 유효 범위의 `최상단에 선언`하는 것

*`var변수 선언`과 `함수선언문`에서만 일어남

```javascript
console.log("hello");
var myname = "HEEE"; // var 변수
```
1. var myname = "HEEE";

2. console.log("hello");

```javascript
ex();
function ex() { // 함수선언문
          console.log("hello");
}
```
1. function ex();  

2. ex();


## 함수의 반환값

return값이 없으면 기본 반환값인 `undefined가 반환됨`

*자바스크립트에는 `void타입이 없음`



## arrow function
ES2015에서 추가된 문법

```javascript
function getName(name){
	return "Kim" + name;
}

// 위 함수와 아래 arrow함수와 같다.
var getName = (name) =>"kim" + name;
```



## 자바스크립트 함수 호출 스택

```javascript
function foo(b){
    var a = 5;
    return a * b + 10;
} 

function bar(x){
    var y = 3;
    return foo(x * y);
}

console.log(bar(6));
```

**Call stack**

1. main()

2. console.log(bar(6))

3. bar(6)

4. foo(18)


---

# Window 객체

많은 메서드가 존재하며`window.method()`에서 `window.`을 생략가능


## setTimeout()

- 인자로 함수를 받는 `콜백함수`

- setTimeout 일정 시간 간격 이후에 함수가 한번 실행됨

- `비동기(asynchronous)로 실행`되어 동기적인 다른 실행이 끝나야 실행됨

```javascript
function run() {
    console.log("start");
    setTimeout(function() {
        var msg = "hello codesquad";
        console.log(msg);  //이 메시지는 즉시 실행되지 않습니다.
    }, 1000);
    console.log("end");
}

run();
```

**실행순서**

1. start

2. end

3. hello codesquad



---


# DOM(Document Object Model)

- 브라우저에서는 HTML코드를 DOM이라는 `객체형태의 모델`로 저장함

- 그렇게 저장된 정보 `DOM Tree`라고 함

- DOM tree를 찾고 조작할 수 있게 도와주는 여러 메서드(`DOM API`)를 제공



## getElementById() 과 querySelector()

DOM API

`getElementById()`: id를 통해 Element 객체를 반환

`querySelector()`: selector의 구체적인 그룹과 일치하는 첫번째  Element 객체를 반환, 더 구체적이고 한정적임



# 이벤트(Event)

## 이벤트 등록

- `addEventListener 함수`를 사용

- addEventListener 함수의 두번째 인자는 이벤트가 발생할 때 실행되는 함수

- `이벤트핸들러(Event Handler)` 또는 `이벤트리스너(Event Listener)`라고 함

```html
<html>
	<header></header>
	<body>
		<div class="outside">outside element</div>
	</body>
	<script src="test.js"></script>
</html>
```

```javascript
var el = document.querySelector(".outside");
el.addEventListener("click", function(){

//do something..

}, false);
```


## 이벤트 객체

이벤트 리스너를 호출할 때, 사용자로부터 어떤 이벤트가 발생했는지에 대한 `정보를 담은 이벤트 객체`를 생성해서 리스너 함수에 전달

```javascript
var el = document.getElementById("outside");

//이벤트 리스너:addEventListener() / 이벤트 객체: evt.target

el.addEventListener("click", function(evt){
	console.log(evt.target);
	console.log(evt.target.nodeName);
}, false);
```


---



# Ajax (Asynchronous Javascript And Xml)

- 브라우저가 가지고있는 XMLHttpRequest 객체를 이용하여 `페이지의 일부`만을 위한 데이터를 로드하는 기법

- 자바스크립트를 통해 서버에 데이터 요청함

*`비동기 방식`: 웹페이지를 리로드하지않고 데이터를 불러오는 방식


## AJAX의 동작 과정

1. 이벤트 발생

2. 자바스크립트 호출

3. XMLHttpRequest 객체 생성 및 서버로 요청

4. 서버의 동작: XML 또는 JSON 형태의 데이터로 웹 브라우저에 전달

5. 서버로 받은 데이터로 자바스크립트 호출

6. 요청한 일부분만 갱신


##  Json 포맷

Ajax를 위한 대표적인 포맷

```Json
{
  "key": "반드시 큰따옴표로 둘러싸야한다",
  "value": "값은 string, number, boolean, array, object, null이 올 수있다",
  "구분": "키와 값은 : 을 이용해 구분하고 키/값 쌍은 , 로 구분한다",
  "name": "Alice",
  "age": 10
}
```




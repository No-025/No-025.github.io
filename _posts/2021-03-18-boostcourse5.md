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

`toString.call()`: 자바스트립트 타입 확인


---



> [자바스크립트 기본문법 참고](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide)



---

# 자바스크립트 함수


## 호이스팅(Hoisting)

함수 안에 있는 선언들을 모두 끌어 올려서
해당 함수 유효 범위의 `최상단에 선언`하는 것

`var변수 선언`과 `함수선언문`에서만 일어남

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

return값이 없으면 기본 반환값인 `undefined`가 반환됨

*자바스크립트에는 void타입이 없음



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

## setTimeout()

setTimeout 일정 시간 간격 이후에 함수가 한번 실행됨

`비동기(asynchronous)로 실행`되어 동기적인 다른 실행이 끝나야 실행됨

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

**console**
1. start

2. end

3. hello codesquad













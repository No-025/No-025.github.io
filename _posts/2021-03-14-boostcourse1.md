---
title: "210314-웹프그래밍 기초"
toc: tru
toc_label: "웹프로그래밍 기초"
categories:
  - Spring
  - HTML
  - CSS
---


## 웹 기초

**HTTP**  
클라이언트가 요청, 서버가 응답  
-장: 많은 요청과 응답 처리가 가능  
-단: 무상태(stateless)

**URL**  
인터넷 상의 자원 위치  

**WEB서버**  
클라이언트가 요청하는 *정적*인 데이터 처리하는 웹서버  

**WAS서버**  
클라이언트가 요청하는 *동적*인 데이터 처리하는 웹서버  
	\*대부분 WAS는 *정적*인 컨텐츠를 제공해줌  

---

## CSS: style을 HTML페이지에 적용하는 3가지 방법

### inline

가장 먼저 적용됨  

```CSS
<p style="border:1px solid gray; color:red; font-size:2em;">
```  

### internal

css파일을 관리할 필요없지만 유지보수 어려움  

```html
<head>
<style>
p  {
  font-size : 2em;
  border:1px solid gray;
  color: red;
}
</style>
</head>
```  

### external

외부파일(.css)로 지정하는 방식(**권장**) 

```html
<head>
	<link rel="stylesheet" href="style.css">
</head>
```  

---

## 캐스케이딩: 작은 계단 모양의 폭포  
- CSS 스타일은 *경쟁*에 의해서 스타일이 적용됨  
- <u>id > class > 엘리먼트</u> 순으로 우선순위를 갖음

---

## 크롬 개발자도구의 Element panel  
- 현재 엘리먼트의 값을 임시로 바꿀 수 있음  
- 최종 결정된 *CSS 값을 확인*할 수 있음


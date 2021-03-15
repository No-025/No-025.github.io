---
title: "boostcourse 풀스택: 웹프그래밍 기초"
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
많은 요청과 응답 처리가 가능하지만 무상태(stateless)이다.

**URL**
인터넷 상의 자원 위치

**WEB서버**
클라이언트가 요청하는 정적인 데이터 처리하는 웹서버

**WAS서버**
클라이언트가 요청하는 동적인 데이터 처리하는 웹서버
대부분 WAS는 정적인 컨텐츠를 제공해줌  

---

## HTML

>html 예제  
>
```
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
</head>
<body>
  <header>
  <h1>Company Name</h1>
  <img src="..." alt="logo">
  </header>
  
  <section id="nav-section">
    <nav><ul>
      <li>Home</li>
      <li>Home</li>
      <li>About</li>
      <li>Map</li>
      </ul>
    </nav>
    
    <section id="roll-section">
      <button></button>
      <div><img src="dd" alt=""></div>
      <div><img src="dd" alt=""></div>
      <div><img src="dd" alt=""></div>
      <button></button>
    </section>
    <section>
      <ul>
        <li class="our_diescriptipn">
          <h3>What we do</h3>
          <div>Lorem ipsum dolor sit amet, consectetur adipisicing</div>
        </li>
        <li class="our_diescriptipn">
          <h3>What we do</h3>
          <div>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Similique accusamus, corporis, dolorum fugiat tenetur porro. Aspernatur commodi, ea suscipit non? Molestiae nulla explicabo debitis provident nostrum dolorem minima reiciendis suscipit?</div>
        </li>
        <li class="our_diescriptipn">
          <h3>What we do</h3>
          <div>Lorem ipsum dolor sit amet, consectetur adipisicing</div>
        </li>
      </ul>
    </section>
  </section>
  <footer>
    <span>Copyright @codesquad</span> 
  </footer>
</body>
</html>
```
---

## CSS: style을 HTML페이지에 적용하는 3가지 방법

1. **inline**: 가장 먼저 적용됨
```
<p style="border:1px solid gray;color:red;font-size:2em;">
```

2. **internal**: 별도의 css파일을 관리할 필요없지만 유지보수 어려움

```
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

3. **external**: 외부파일(.css)로 지정하는 방식으로 짧지않다면 권유하는 방식

```
<head>
	<link rel="stylesheet" href="style.css">
</head>
```

---



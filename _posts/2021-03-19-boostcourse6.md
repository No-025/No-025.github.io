---
title: "210319-JSP"
toc: tru
toc_label: "DB"
categories:
  - JSP
---

---

# JSP

- 서블릿의 단점을 보완하고자 만든 서블릿 기반의 스크립트 기술

- JSP가 실행되는 것이 아니라 서블릿으로 바뀜


```JSP
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
</head>
<body>

<% 
    int total = 0;
    for(int i = 1; i <= 10; i++){
        total = total + i;
    }
%>

1부터 10까지의 합 : <%=total %>

</body>
</html>
```



## 서블릿과 JSP 비교

기능의 차이는 없고 `역할의 차이`


### Servlet
- Java 코드 안에 HTML코드
- HTML 태그를 `("")`안에 처리
- DB와 통신, 데이터를 읽고 확인하기 등 Controller에 좋음
- 수정시, 전체 코드를 업데이트하고 다시 컴파일한 후 재배포하는 작업이 필요하여 `개발 생산성 저하`



### JSP
- HTML 코드안에 Java코드
- 자바 코드를 `<% %>` 안에 처리
- html과 같은 View에 좋음
- 수정시, 재배포 필요없이 WAS가 알아서 처리



## JSP 실행순서

1.  브라우저가 웹서버에 JSP에 대한 요청 정보를 전달한다.

2.  브라우저가 요청한 JSP가 `최초로 요청`했을 경우만 JSP로 작성된 코드가 `서블릿으로` 코드로 변환한다. (`java 파일 생성`)

3.  `서블릿 코드를 컴파일`해서 실행가능한 bytecode로 변환한다. (`class 파일 생성`)

4.  서블릿 클래스를 로딩하고 `인스턴스를 생성`한다.

5.  `서블릿이 실행`되어 요청을 처리하고 응답 정보를 생성한다.



## JSP 라이프 싸이클

서블릿과 동일

`Init() 호출` -> 최초 한번

`service()` -> 요청시 매번

`destroy() 호출` -> 마지막 한번

## JSP 문법

`<% %>` - 스크립트릿, 프로그래밍 코드 기술
  
`<%= %>` - 익스프레션, 화면에 출력할 내용 기술

`<%! %> ` - 선언문, 전역변수 선언 및 메소드 선언 기술
  
`<%@ %>` - 지시자, 웹컨테이너가 jsp 페이지를 처리할 때 필요한 정보를 기술  


```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8 "
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="EUC-KR">
<title>Insert title here</title>
</head>
<body>
	<%
	for (int i = 1; i <= 5; i++) {
	%>
	<H <%=i%>> 아름다운 한글 </H<%=i%>>
	<%
	}
	%>
</body>
</html>
```



## 주석

JSP페이지에서 사용할 수 있는 주석

> HTML주석, 자바주석, JSP주석


1. HTML 주석

`<!--  -->`

```html
<!-- html 주석입니다. -->
```

2. JSP 주석

`<%--  --%>`

```jsp
<%-- JSP 주석입니다. --%>
```

3. Java 주석

`//, /*  */`

```java
//Java 주석입니다.

/*Java
주석입니다.*/
```


## JSP 내장 객체

- JSP가 서블릿 소스로 생성되고 실행될 때, _jspService()에 삽입된 코드의 윗부분에 `미리 선언된 객체들`

- jsp에도 사용 가능

- response, request, application, session, out 등


---


# 리다이렉트 (redirect)

- HTTP프로토콜로 정해진 규칙

- 서버가 클라이언트의 요청에 대해 `특정 URL로 이동`을 요청



## 리다이렉트 예제

>redirect01.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%
	response.sendRedirect("redirect02.jsp");

%>
```jsp


>redirect02.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>redirect된 페이지입니다.
</body>
</html>
```

![Redirect](/assets/images/210319red.png "Redirect") 

**(출처: 부스트코스)**



---


# forward

서블릿이나 JSP가  request의 추가 처리를 위해 `다른 서블릿이나 JSP`에 정보 전달

## forward 예제


>FrontServlet


```java
protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	// TODO Auto-generated method stub
	int diceValue = (int) (Math.random() * 6) + 1;
	request.setAttribute("dice", diceValue);

	RequestDispatcher requestDispatehcer = request.getRequestDispatcher("/next");
	requestDispatehcer.forward(request, response);
}
```


>NextServlet.java


```java
protected void service(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	response.setContentType("text/html");
	PrintWriter out = response.getWriter();
	out.println("<html>");
	out.println("<head><title>form</title></head>");
	out.println("<body>");
	int dice = (Integer) request.getAttribute("dice");
	out.println("dice : " + dice);
	for (int i = 0; i < dice; i++) {
		out.print("<br>hello");
	}
	out.println("</body>");
	out.println("</html>");
}
```

![Forward](/assets/images/210319fow.png "Forward") 

**(출처: 부스트코스)**


---


# redirect와 forward 차이

- redirect는 URL이 변경되고, request 객체를 재사용하지 않음
*2개의 request

- forward는 URL이 변경되지 않습니다. request 객체를 재사용
*1개의 request

> 시스템에 변화가 생기는 요청은 `redirect`, 그렇지 않으면 `forward`



---


# servlet과 JSP 연동

프로그램 로직 수행은 Servlet에서, 결과 출력은 JSP에서 하는 것이 유리
 

> `Servlet에서 프로그램 로직`이 수행되고, 그 결과를 `JSP에게 포워딩`



## servlet과 JSP 연동 예제

> LogicServlet.java
> 

```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	// TODO Auto-generated method stub
	int v1 = (int)(Math.random() * 100) + 1;
	int v2 = (int)(Math.random() * 100) + 1;
        int result = v1 + v2;
        
        request.setAttribute("v1", v1);
        request.setAttribute("v2", v2);
        request.setAttribute("result", result);
        
        RequestDispatcher requestDispatcher = request.getRequestDispatcher("/result.jsp");
        requestDispatcher.forward(request, response);
}
```


> result.jsp
> 

```jsp
<body>
스클립틀릿과 표현식을 이용해 출력합니다.<br>
<%
    int v1 = (int)request.getAttribute("v1");
    int v2 = (int)request.getAttribute("v2");
    int result = (int)request.getAttribute("result");
%>

<%=v1%> + <%=v2 %> = <%=result %>

</body>
```



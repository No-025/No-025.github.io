---
title: "210321-Scope와 JSTL와 EL"
toc: tru
toc_label: "Scope와 JSTL EL"
categories:
  - JSP
---

---

# 1. Scope

웹 애플리케이션 내에서 4개의 객체 범위

`Page < Request < Session < Application`

## - Page Scope

한 번의 request를 처리하는 `하나의 JSP페이지`내에서 저장 및 공유하기 위해서 사용

-  해당 페이지가 클라이언트에 서비스를 제공하는 동안만 유효
- JSP 페이지에서 `pageContext`라는 내장 객체로 사용 가능  
- 페이지 내에서 `지역변수`처럼 사용




## - Request Scope

한 번의 reqeust를 처리하는 데 사용되는 `모든 JSP페이지`에서 저장 및 공유하기 위해서 사용

- 클라이언트의 요청이 처리되는 동안 유효
- JSP에서는 `request` 내장 변수를 사용
- Servlet에서는 `HttpServletRequest` 객체를 사용
- `forward` 시 값을 유지하고자 사용




## - Session Scope

로그인 정보같은 `한 명의 uesr`와 관련된 정보를 저장 및 공유하기 위해서 사용

- 세션이 유지되는 동안 유효
- JSP에서는 `session` 내장 변수를 사용
- Servlet에서는 HttpServletRequest의 `getSession()` 메소드 사용
- 웹 브라우저간의 탭 간에는 세션정보(상태정보)가 공유



## - Application Scope

게시판같이 `모든 사용자`와 관련된 정보를 저장 및 공유하기 위해서 사용

- 웹 애플리케이션이 실행되는 동안 유효
- JSP에서는 `application` 내장 객체를 사용
- Servlet의 경우는 `getServletContext()` 메소드를 사용



### Application Scope 예제

> ApplicationScope01.java


```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
	PrintWriter out = response.getWriter();
	ServletContext application = getServletContext();
	int value = 1;
	application.setAttribute("value", value);

	out.println("<h1>value : " + value + "</h1>");
}
```

---


> ApplicationScope02.java

```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		PrintWriter out = response.getWriter();
		ServletContext application = getServletContext();
		try {
			int value = (int) application.getAttribute("value");
			value++;
			application.setAttribute("value", value);
			out.println("<h1>value : " + value + "</h1>");
		} catch (NullPointerException ex) {
			out.println("value가 설정되지 않습니다.");
		}
}
```

---

> applicationscope01.jsp

```java
<body>
	<%
	try {
		int value = (int) application.getAttribute("value");
		value = value + 2;
		application.setAttribute("value", value);
	%>
	<h1><%=value%></h1>
	<%
	} catch (NullPointerException ex) {
	%>
	<h1>설정된 값이 없습니다.</h1>
	<%
	}
	%>
</body>
```

---

# 2. EL

값을 표현하는 데 사용되는 스크립트 언어로서 JSP의 기본 문법을 보완하는 역할을 하는 
`표현언어`



## - 표현 언어가 제공하는 기능

-   JSP의 `스코프(scope)에 맞는 속성` 사용
-   집합 객체에 대한 접근 방법 제공
-   수치 연산, 관계 연산, 논리 연산자 제공
-   자바 클래스 `메소드 호출` 기능 제공
-   표현언어만의 기본 객체 제공



## - 표현언어의 표현방법

> ${expr }

```java
<b>${session.Scope.memeber.id}</b>님 환영합니다!
```


## - 표현 언어의 데이터 타입

-   불리언 타입
-   정수타입 - 음수의 경우 '-'가 붙음
-   실수타입 - 3.24e3과 같이 지수형으로 표현 가능
-   문자열 타입 - 작은 따옴표(')를 사용해서 표현할 경우  \' 와 같이 \ 기호와 함께 사용
-   \ 기호 자체는 \\ 로 표시한다.
-   널 타입 - null


## - 객체 접근 규칙

>${<표현1>,<표현2>}

-   표현 1이나 표현 2가 `null이면 null을 반환`
-   표현1이 `Map`일 경우 표현2를 `key로한 값을 반환`
-   표현1이 `List나 배열`이면 표현2가 정수일 경우 `해당 정수 번째 index에 해당하는 값`을 반환
-   만약 `정수가 아닐 경우에는 오류`가 발생
-   표현1이 `객체일 경우`는 표현2에 해당하는 `getter메소드에 해당하는 메소드를 호출`한 결과를 반환



## - 표현 언어 비활성화 : JSP에 명시하기

```java
<%@ page isELIgnored = "true" %>
```



### EL 예제

```java
<%
    pageContext.setAttribute("p1", "page scope value");
    request.setAttribute("r1", "request scope value");
    session.setAttribute("s1", "session scope value");
    application.setAttribute("a1", "application scope value");
    request.setAttribute("k", 10);
    request.setAttribute("m", true);
%>  

...

<body>
pageContext.getAttribute("p1") : ${pageScope.p1 }<br>
request.getAttribute("r1") : ${requestScope.r1 }<br>
session.getAttribute("s1") : ${sessionScope.s1 }<br>
application.getAttribute("a1") : ${applicationScope.a1 }
k : ${k } <br>
k + 5 : ${ k + 5 } <br>
k - 5 : ${ k - 5 } <br>
k * 5 : ${ k * 5 } <br>
k / 5 : ${ k div 5 } <br>

k : ${k }<br>
m : ${m }<br>
k > 5 : ${ k > 5 } <br>
k < 5 : ${ k < 5 } <br>
k <= 10 : ${ k <= 10} <br>
k >= 10 : ${ k >= 10 } <br>
m : ${ m } <br>
!m : ${ !m } <br>
</body>
```

---


# 3. JSTL

JSP 페이지에서 조건문 처리, 반복문 처리 등을 `html tag형태`로 작성할 수 있는 JSP 확장태그



## - JSTL 사용하기

[ JSTL 1.2.5](http://tomcat.apache.org/download-taglibs.cgi)

WEB-INF/lib 밑에 jar 파일을 넣어줌

- taglibs-standard-impl-1.2.5.jar

- taglibs-standard-spec-1.2.5.jar

- taglibs-standard-jstlel-1.2.5.jar


## - JSTL 코어태그

```java
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> 
```

접두어: c

- 변수지원
- 흐름제어
- URL 처리


## - 코어 태그: 변수 지원 태그 - set, remove

> set, remove 문법

```java
<c:set var="valName" scope="session" value="someValue"/>
<c:remove var="varName" scope="session" />
```
- var: EL에서 사용될 변수명
- scope: 변수값이 저장될 영역 (page, request, session, application)
- value: 변수값

## - set, remove 예제


```java
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> 

<c:set var="value1" scope="request" value="kang"/>

...

<body>

성 : ${value1} <br>

<c:remove var="value1" scope="request"/>

성 : ${value1 }
</body>
```

---

## - 코어 태그: 변수 지원 태그 - 프로퍼티, 맵의 처리


> 프로퍼티, 맵의 처리 문법

```java
<c:set target="${some}" property="propertyName" value="anyValue"/>
```
some 객체가 `자바빈`일 경우, `some.setPropertyName(antValue)`
some 객체가 `맵`일 경우, `some.put(propertyName, anyValue);`


- target: <c:set>으로 지정한 변수 객체
- property: 프로퍼티 이름
- value: 새로 지정할 프로퍼티 값






## - 코어 태그: 흐름제어 태그 - if

> if 문법

```java
<c:if test="조건">
</c:if>
```

###  if 예제

```java
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> 
<%
request.setAttribute("n", 10);
%>

...
<body>
<c:if test="${n == 0}">
n은 과 0과 같습니다.
</c:if>

<c:if test="${n == 10}">
n은 과 10과 같습니다.
</c:if>
</body>
```

---


## - 코어 태그: 흐름제어 태그 - choose

> choose 문법

```java
<c:choose>
	<c:when test="조건1">
	</c:when>
	<c:when test="조건2">
	</c:when>
	<c:otherwise>
	</c:otherwise>
</c:choose>
```

### choose 예제


```java
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> 
<%@ page import="java.util.*" %>
<%
    request.setAttribute("score", 83);
%>

...

<body>
<c:choose>
    <c:when test="${score >=90 }">
    A학점입니다.
    </c:when>
    <c:when test="${score >=80 }">
    B학점입니다.
    </c:when>
    <c:when test="${score >=70 }">
    C학점입니다.
    </c:when>
    <c:when test="${score >=60 }">
    D학점입니다.
    </c:when>
    <c:otherwise>
    F학점입니다.
    </c:otherwise>            
</c:choose>
</body>
```


## - 코어 태그: 흐름제어 태그 - forEach

> forEach 문법

```java
<c:forEach var="변수" items="아이템" [begin="시작번호"] [end="끝번호"]>
${변수}
</c:forEach>
```

- var: EL에서 사용될 변수명
- items: 배열, List, Iterator, Enumeration, Map등의 Colletion
- begin: items에 지정한 목록에서 값을 읽어어올 인덱스의 시작값
- end: items에 지정한 목록에서 값을 읽어어올 인덱스의 끝값



### forEach 예제

```java
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> 
<%@ page import="java.util.*" %>
<%
    List<String> list = new ArrayList<>();
    list.add("hello");
    list.add("world");
    list.add("!!!");
    request.setAttribute("list", list);
%>

...

<body>
<c:forEach items="${list}" var="item">
${item } <br>
</c:forEach>
</body>
```

---


## - 코어 태그: 흐름제어 태그 - import

> import 문법

```java
<c:import url="URL" var="변수명" scope="범위">
</c:import>
```

- url: 결과를 읽어올 URL
- var: 읽어온 결과를 저장할 변수명
- scope: 변수를 저장할 영역

### import 예제

```java
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> 
<%@ page import="java.util.*" %>
<c:import url="https://www.google.co.kr/" var="urlValue" scope="request"></c:import>

...

<body>
읽어들인 값 : ${urlValue}
</body>
```

---


## - 코어 태그: 흐름제어 태그 - redirect

> redirect 문법

```java
<c:redirect url="리다이렉트할 URL">
</c:redirect>
```

-url: 리다이렉트할 URL


### redirect 예제

```java
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %> 
<c:redirect url="jstlRedirectPage.jsp"></c:redirect>

...

<h1> redirect된 화면입니다.</h1>
```


---

## - 코어 태그: 기타태그 - out

> out 문법

```java
<c:out value="value" escapeXml="{true | false}" default="defaultValue" />
```

- value: JspWriter에 출력할 값
- escapeXml: 문자를 변경함, 생략할 경우 기본값은 true
- default: value 속성에서 지정한 값이 존재하지 않을 때 사용될 값을 지정


### out 예제

```java
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions"%> 

...

<body>
<c:set var="t" value="<script type='text/javascript'>alert(1);</script>" />
${t}
<c:out value="${t}" escapeXml="true" />
<c:out value="${t}" escapeXml="false" />
</body>
```





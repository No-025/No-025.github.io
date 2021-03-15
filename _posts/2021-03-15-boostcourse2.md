---
title: "boostcourse 풀스택: 서블릿"
toc: tru
toc_label: "서블릿"
categories:
  - Spring
  - Servlet
---

## Servlet이란?

자바 웹 어플리케이션의 구성요소 중 **동적인 처리**를 하는 프로그램의 역할  
**WAS**에서 동작하는 java클래스  
**HttpServlet클래스**를 상속받아야 함  
**HTML은 JSP로** 표현, **복잡한 프로그래밍은 서블릿**으로 구현  
  
  
---
  
  
## Servlet 작성방법

1. **3.0이상** 버전
자바 어노테이션(annotation) 사용(@을 앞에 붙인)  
> 3.1 버전  
> 
```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	response.setContentType("text/html;charset=UTF-8"); // 응답 컨텐츠 타입 지정
	PrintWriter out = response.getWriter(); // 문자열을 출력할 수 있는 PrintWriter 구함
	out.print("<h1>1-10까지 출력</h1>");
	for(int i = 0; i < 10; i++){
		out.println(i+1 + "<br>");
	}
	out.close();
}
```  
   
  
---
  
          
2. **3.0이하** 버전

web.xml파일에 등록  
>2.5버전 web.xml  
>  
```xml
<?xml version="1.0" encoding="UTF-8"?>
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xmlns="http://java.sun.com/xml/ns/javaee" 
xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" version="2.5">
    <display-name>exam25</display-name>
    <welcome-file-list>
        <welcome-file>index.html</welcome-file>
        <welcome-file>index.htm</welcome-file>
        <welcome-file>index.jsp</welcome-file>
        <welcome-file>default.html</welcome-file>
        <welcome-file>default.htm</welcome-file>
        <welcome-file>default.jsp</welcome-file>
    </welcome-file-list>
    <servlet>
        <description></description>
        <display-name>TenServlet</display-name>
        <servlet-name>TenServlet</servlet-name>
        <servlet-class>exam.TenServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>TenServlet</servlet-name>
        <url-pattern>/ttt</url-pattern>
    </servlet-mapping>
</web-app>
```  
  
  
---
  
  
## Serverlet 라이프사이클

**Servlet 객체 생성**: 최초 *한번*  
**Init() 호출** -> 최초 *한번*  
**service(), doGet(), doPost() 호출** -> 요청시 *매번*  
**destroy() 호출** -> 마지막 *한번* (servlet 수정, 서버 재가동 등)  
   
  
---
  
  
  
## WAS가 웹브라우저로부터 요청 받으면

![Was](/assets/images/210315was.png "Was")  
*(출처: boostcourse)*  

1. 요청할 때 가지고 들어온 다양한 정보들을  HttpServletRequest객체를 생성하여 저장
2. 웹 브라우저에 응답을 보낼 정보들을  HttpServletResponse객체를 생성하여 저장
3. 생성된 HttpServletRequest, HttpServletResponse 객체를 서블릿에게 전달

----------

## Header정보 읽어 들이기

```java
/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		response.setContentType("text/html");
		PrintWriter out = response.getWriter();
		out.println("<html>");
		out.println("<head><title>form</title></head>");
		out.println("<body>");

		Enumeration<String> headerNames = request.getHeaderNames();
		while(headerNames.hasMoreElements()) {
			String headerName = headerNames.nextElement();
			String headerValue = request.getHeader(headerName);
			out.println(headerName + " : " + headerValue + " <br> ");
		}		
		
		out.println("</body>");
		out.println("</html>");
	}

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		doGet(request, response);
	}	
```
  
---
  
## 파라미터 읽어 들이기
URL주소의 파라미터 정보를 읽어 들여 브라우저 화면에 출력함  
  
```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	response.setContentType("text/html");
	PrintWriter out = response.getWriter();
	out.println("<html>");
	out.println("<head><title>form</title></head>");
	out.println("<body>");
	
	String name = request.getParameter("name");
	String age = request.getParameter("age");
	
	out.println("name : " + name + "<br>");
	out.println("age : " +age + "<br>");
		
	out.println("</body>");
	out.println("</html>");
}
```  

>파라미터가 없는 경우
>
![Parax](/assets/images/210315parax.png "Parax")  

>파라미터가 있는 경우
>
![Parao](/assets/images/210315parao.png "Parao")  
  
---
  
## 그외의 요청정보 출력하기

```java
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
		response.setContentType("text/html");
		PrintWriter out = response.getWriter();
		out.println("<html>");
		out.println("<head><title>info</title></head>");
		out.println("<body>");

		String uri = request.getRequestURI();
		StringBuffer url = request.getRequestURL();
		String contentPath = request.getContextPath();
		String remoteAddr = request.getRemoteAddr();
		
		
		out.println("uri : " + uri + "<br>");
		out.println("url : " + url + "<br>");
		out.println("contentPath : " + contentPath + "<br>");
		out.println("remoteAddr : " + remoteAddr + "<br>");
		
		out.println("</body>");
		out.println("</html>");
	}
```
로컬 서버이기때문에 *0:0:0:0:0:0:0:1*

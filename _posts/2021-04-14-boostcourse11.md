---
title: "Todo-List"
toc: tru
toc_label: "Todo-List"
categories:
  - Project
---


---


# 1. AJAX


## - 서버에 요청하기
> XMLHttpRequest 객체를 사용하여 서버와 데이터 교환
```
var oReq = new XMLHttpRequest();
```

## - open()메소드
> 서버로 보낼 Ajax 요청의 형식을 설정
```
open(전달방식, URL주소, 동기,비동기여부);
```

> 전달방식: GET 방식

```
//parameter를 붙여서 보낼수있음.
oReq.open('GET', '/Todo/todoType?id=' + id + '&type=' + type);
oReq.send();
```

> 전달방식: POST 방식

```
// POST 방식의 요청은 데이터를 Http 헤더에 포함시켜 전송함. 
oReq.open("POST", oReq.open("POST", "./TodoTypeServlet", true);
oReq.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
oReq.send("id=" + id + "&type=" + type);
```


## - 서버로부터 응답 확인

> readyState 프로퍼티: 객체의 현재 상태

1. **0 (uninitialized)**: (request가 초기화되지 않음)

2. **1 (loading)**:  (서버와의 연결이 성사됨)

3. **2 (loaded)**: (서버가 request를 받음)

4. **3 (interactive)**: (request(요청)을 처리하는 중)

5.  **4 (complete)**:  (request에 대한 처리가 끝났으며 응답할 준비가 완료됨)

```
if (httpRequest.readyState === XMLHttpRequest.DONE) {
    // 이상 없음, 응답 받았음
} else {
    // 아직 준비되지 않음
}
```

---

> status 프로퍼티: 서버의 문서 상태

1. **200** : 서버에 문서가 존재함

2.  **404** : 서버에 문서가 존재하지 않음

3.  **500**: 서버에 예측 못한 문제가 발생함

```
if (httpRequest.status === 200) {
    // 이상 없음!
} else {
    // 요구를 처리하는 과정에서 문제가 발생되었음
    // 예를 들어 응답 상태 코드는 404 (Not Found) 이거나
    // 혹은 500 (Internal Server Error) 이 될 수 있음
}
```

## - 새로고침
```
function refresh(){
		location.reload();
	}
```

---


# 2. HTML

## - POST
```
<form action= "./TodoAddServlet" method="post" >
```

---


# 3. JSTL

## - foreach

```
<c:forEach var="todoType" items="${todoType}">
...
</c:forEach>
```

## - if

```
<c:if test="${todoList.type == todoType}">
...
</c:if>
```


---

# 4. Servlet

## - forwoard

```
RequestDispatcher requestDispatcher = request.getRequestDispatcher("main.jsp");
requestDispatcher.forward(request, response);
```


## - redirect

```
resp.sendRedirect("./MainServlet");
```

---


# 5. SQL

## - 생성
```
CREATE TABLE todo ( 
id BIGINT(20) UNSIGNED NOT NULL AUTO_INCREMENT, 
title VARCHAR(255) NOT NULL, 
name VARCHAR(100) NOT NULL, 
sequence INT(1) NOT NULL, 
type VARCHAR(20) DEFAULT 'TODO', 
regdate DATETIME DEFAULT NOW(), 
PRIMARY KEY (id) 
);
```


## - 입력

```
insert into todo(title, name, sequence) 
values('자바스크립트공부하기', '홍길동', 1); 
```

## - 수정

```
update todo set type = 'DOING' where id = 1; 
```


## - 조회

```
select id, title, name, sequence, type, regdate from todo 
order by regdate desc
```

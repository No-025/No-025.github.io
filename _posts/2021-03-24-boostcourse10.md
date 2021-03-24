 ---
title: "210324-오류 해결"
toc: tru
toc_label: "오류해결"
categories:
  - Eclipse
---


---



[Web API 예제](https://no-025.github.io/maven/jdbc/api/boostcourse9/)


# 1. org.~.core.xml이 없을 때

1. `propertices` > `Project Facets` >  `convert to...`
2. `dynamic web module` 추가
3. 버전 3.1로 변경


# 2. maven 라이브러리 해결

## - 문제

 도중 `HTTP 상태 500 – 내부 서버 오류` 발생

> java.lang.ClassNotFoundException: ~jdbcDriver

> No suitable driver found for jdbc:mysql://~주소

> java.lang.ClassNotFoundException: com.fasterxml.jackson.databind.ObjectMapper

1. jdbc drive를 찾지 못함
2. mysql 연결이 안됨
3. ObjectMapper을 찾지 못함

---

## - 이유

Maven > Update Project Configuration 실행시 maven 라이브러리 경로가 삭제됨

---

## - 해결

1. `properties` >  `Deployment Assembly` > `Add`
2. `Java Build Path Entries` > `Maven Dependencies` > `Apply`




---
title: "210316-이클립스로 실행한 html에 css가 적용 안 될 때"
toc: tru
toc_label: "CSS 적용하기"
categories:
  - Eclipse
  - HTML
  - CSS
---

## 이클립스에서 CSS 적용하기

이클립스 Run as로 html을 켜면 css가 적용 안될 때가 있다.

그럴땐,  

`톰캣 경로와 이클립스 경로를 맞춰주자`  

1. 이클립스 Project Explore을 연다.
2. 이클립스에 연결한 톰캣파일을 연다.
3. server.xml파일을 연다.

```xml
 <Host appBase="webapps" autoDeploy="true" name="localhost" unpackWARs="true">
```

"webapps"부분에 이클립스 경로를 넣어준다.

```xml
 <Host appBase="D:\eclipse-workspace\aboutme" autoDeploy="true" name="localhost" unpackWARs="true">
```
  
  
이제 CSS가 적용된 html이 보일 것이다.

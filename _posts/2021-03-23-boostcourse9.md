---
title: "210323-Maven과 JDBC, API"
toc: tru
toc_label: "Maven과 JDBC, API"
categories:
  - Maven
  - JDBC
  - API
---

---
# 1. Maven

빌드(Build), 패키징, 문서화, 테스트와 테스트 리포팅, git, 의존성관리, svn등과 같은 `형상관리서버와 연동(SCMs), 배포` 등의 작업을 손쉽게 할 수 있음


## - CoC(Convention over Configuration)

`일종의 관습`

- 프로그램의 소스파일은 어떤 위치에 있어야 하는가?
- 소스가 컴파일된 파일들은 어떤 위치에 있어야 하는가?

## - Maven 문법

``` xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>kr.or.connect</groupId>
	<artifactId>jdbcexam</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>war</packaging>

	<name>jdbcexam Maven Webapp</name>
	<!-- FIXME change it to the project's website -->
	<url>http://www.example.com</url>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<maven.compiler.source>1.7</maven.compiler.source>
		<maven.compiler.target>1.7</maven.compiler.target>
	</properties>

	<dependencies>
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.11</version>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<finalName>jdbcexam</finalName>
		<pluginManagement><!-- lock down plugins versions to avoid using Maven 
				defaults (may be moved to parent pom) -->
			<plugins>
				<plugin>
					<artifactId>maven-clean-plugin</artifactId>
					<version>3.1.0</version>
				</plugin>
				<!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
				<plugin>
					<artifactId>maven-resources-plugin</artifactId>
					<version>3.0.2</version>
				</plugin>
				<plugin>
					<artifactId>maven-compiler-plugin</artifactId>
					<version>3.8.0</version>
				</plugin>
				<plugin>
					<artifactId>maven-surefire-plugin</artifactId>
					<version>2.22.1</version>
				</plugin>
				<plugin>
					<artifactId>maven-war-plugin</artifactId>
					<version>3.2.2</version>
				</plugin>
				<plugin>
					<artifactId>maven-install-plugin</artifactId>
					<version>2.5.2</version>
				</plugin>
				<plugin>
					<artifactId>maven-deploy-plugin</artifactId>
					<version>2.8.2</version>
				</plugin>
			</plugins>
		</pluginManagement>
	</build>
</project>
```


-   **project**  : pom.xml 파일의 `최상위 루트 엘리먼트`(Root Element)  
    
-   **modelVersion**  : `POM model의 버전`
    
-   **groupId**  : 프로젝트를 생성하는 `조직의 고유 아이디`
*일반적으로 도메인 이름을 거꾸로 적음
    
-   **artifactId**  : 해당 프로젝트에 의하여 생성되는 `artifact의 고유 아이디`
    
-   **packaging**  : 해당 프로젝트를 `어떤 형태로 packaging`(jar, war, ear)
    
-   **version**  : `프로젝트의 현재 버전` 
    
-   **name**  : `프로젝트의 이름`  
    
-   **url**  : 프로젝트 사이트가 있다면 `사이트 URL`을 등록



# 2. JDBC


`자바 프로그램 내에서 SQL문을 실행하기 위한 자바 API`


## - JDBC 프로그래밍 순서

1.  import java.sql.*;
2.  드라이버를 로드
3.  Connection 객체 생성
4.  Statement 객체 생성 및 질의 수행
5.  SQL문에 결과물이 있다면 ResultSet 객체를 생성
6.  모든 객체를 닫음(**중요**)


> import


```java
import java.sql.*;
```

---


> 드라이버 로드

```java
Class.forName( "com.mysql.jdbc.Driver" );
```


---


> Connection 얻기

```java
String dburl  = "jdbc:mysql://localhost/dbName";

Connection con =  DriverManager.getConnection ( dburl, ID, PWD );
```


---


> Statement 생성

```java
Statement stmt = con.createStatement();
```


---


> 질의 수행

```java
ResultSet rs = stmt.executeQuery("select no from user" );

참고
stmt.execute(“query”);             //any SQL
stmt.executeQuery(“query”);     //SELECT
stmt.executeUpdate(“query”);   //INSERT, UPDATE, DELETE
```


---


> ResultSet으로 결과 받기

```java
ResultSet rs =  stmt.executeQuery( "select no from user" );
while ( rs.next() )
      System.out.println( rs.getInt( "no") );
```


---


> Close

```java
rs.close();

stmt.close();

con.close();
```



## - JDBC 조건문 조회

> pom.xml

```xml
<!-- 추가 -->
<dependency>
	<groupId>mysql</groupId>
	<artifactId>mysql-connector-java</artifactId>
	<version>8.0.23</version>
</dependency>
``` 

---


> Role.java

```java
package kr.or.connect.jdbcexam.dto;

public class Role {
	private Integer roleId;
	private String description;
	
	public Role() {
		
	}

	public Role(Integer roleId, String description) {
		// TODO Auto-generated constructor stub
		super();
		this.roleId = roleId;
		this.description = description;
	}

	public Integer getRoleId() {
		return roleId;
	}

	public void setRoleId(Integer roleId) {
		this.roleId = roleId;
	}

	public String getDescription() {
		return description;
	}

	public void setDescription(String description) {
		this.description = description;
	}

	@Override
	public String toString() {
		return "Role [roleId=" + roleId + ", description=" + description + "]";
	}
}
```

---

> RoleDao.java

```java
package kr.or.connect.jdbcexam.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

import kr.or.connect.jdbcexam.dto.Role;

public class RoleDao {
	private static String dburl = "jdbc:mysql://localhost:3306/connectdb";
	private static String dbUser = "connectuser";
	private static String dbpasswd = "connect123!@#";

	public Role getRole(Integer roleId) {
		Role role = null;
		Connection conn = null;
		PreparedStatement ps = null;
		ResultSet rs = null;

		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
			conn = DriverManager.getConnection(dburl, dbUser, dbpasswd);
			String sql = "SELECT description,role_id FROM role WHERE role_id = ?";
			ps = conn.prepareStatement(sql);
			ps.setInt(1, roleId);
			rs = ps.executeQuery();

			if (rs.next()) {
				String description = rs.getString(1);
				int id = rs.getInt("role_id");
				role = new Role(id, description);
			}
		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			if (rs != null) {
				try {
					rs.close();
				} catch (SQLException e) {
					e.printStackTrace();
				}
			}
			if (ps != null) {
				try {
					ps.close();
				} catch (SQLException e) {
					e.printStackTrace();
				}
			}
			if (conn != null) {
				try {
					conn.close();
				} catch (SQLException e) {
					e.printStackTrace();
				}
			}
		}

		return role;
	}
}
```

---

> JDBCExam1.java

```java
package kr.or.connect.jdbcexam;

import kr.or.connect.jdbcexam.dao.RoleDao;
import kr.or.connect.jdbcexam.dto.Role;

public class JDBCExam1 {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		RoleDao dao = new RoleDao();
		Role role = dao.getRole(100);
		System.out.println(role);
	}

}
```


## -JDBC 한 행 입력


> RoleDao.java

```java
package kr.or.connect.jdbcexam.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;

import kr.or.connect.jdbcexam.dto.Role;

public class RoleDao {
	private static String dburl = "jdbc:mysql://localhost:3306/connectdb";
	private static String dbUser = "connectuser";
	private static String dbpasswd = "connect123!@#";

	public int addRole(Role role) {
		int insertCount = 0;

		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		}
		String sql = "INSERT INTO role (role_id, description) VALUES ( ?, ? )";

		try (Connection conn = DriverManager.getConnection(dburl, dbUser, dbpasswd);
				PreparedStatement ps = conn.prepareStatement(sql)) {

			ps.setInt(1, role.getRoleId());
			ps.setString(2, role.getDescription());

			insertCount = ps.executeUpdate();

		} catch (Exception ex) {
			ex.printStackTrace();
		}
		return insertCount;
	}
}
```


---

> JDBCExam2.java


```java
package kr.or.connect.jdbcexam;

import kr.or.connect.jdbcexam.dao.RoleDao;
import kr.or.connect.jdbcexam.dto.Role;

public class JDBCExam2 {
	public static void main(String[] args) {
		int roleId = 501;
		String description = "CTO";
		
		Role role = new Role(roleId, description);
		
		RoleDao dao = new RoleDao();
		int insertCount = dao.addRole(role);

		System.out.println(insertCount);
	}
}
```

## -JDBC 모두 조회


> RoleDao.java

```java
package kr.or.connect.jdbcexam.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;

import kr.or.connect.jdbcexam.dto.Role;

public class RoleDao {
	private static String dburl = "jdbc:mysql://localhost:3306/connectdb";
	private static String dbUser = "connectuser";
	private static String dbpasswd = "connect123!@#";

	public List<Role> getRoles() {
		List<Role> list = new ArrayList<>();

		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		}

		String sql = "SELECT description, role_id FROM role order by role_id desc";
		try (Connection conn = DriverManager.getConnection(dburl, dbUser, dbpasswd);
				PreparedStatement ps = conn.prepareStatement(sql)) {

			try (ResultSet rs = ps.executeQuery()) {

				while (rs.next()) {
					String description = rs.getString(1);
					int id = rs.getInt("role_id");
					Role role = new Role(id, description);
					list.add(role); // list에 반복할때마다 Role인스턴스를 생성하여 list에 추가한다.
				}
			} catch (Exception e) {
				e.printStackTrace();
			}
		} catch (Exception ex) {
			ex.printStackTrace();
		}
		return list;
	}
}
```

---

> JDBCExam3.java

```java
package kr.or.connect.jdbcexam;

import java.util.List;

import kr.or.connect.jdbcexam.dao.RoleDao;
import kr.or.connect.jdbcexam.dto.Role;

public class JDBCExam3 {
	public static void main(String[] args) {

		RoleDao dao = new RoleDao();
		
		List<Role> list = dao.getRoles();

		for(Role role : list) {
			System.out.println(role);
		}
	} 
}
```


## -JDBC 한 행 삭제

>RoleDao.java

```java
package kr.or.connect.jdbcexam.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;

import kr.or.connect.jdbcexam.dto.Role;

public class RoleDao {
	private static String dburl = "jdbc:mysql://localhost:3306/connectdb";
	private static String dbUser = "connectuser";
	private static String dbpasswd = "connect123!@#";

	public int deleteRole(Integer roleId) {
		int deleteCount = 0;
		
		Connection conn = null;
		PreparedStatement ps = null;
		
		try {
			Class.forName( "com.mysql.cj.jdbc.Driver" );
			
			conn = DriverManager.getConnection ( dburl, dbUser, dbpasswd );
			
			String sql = "DELETE FROM role WHERE role_id = ?";

			ps = conn.prepareStatement(sql);
			
			ps.setInt(1,  roleId);

			deleteCount = ps.executeUpdate();

		}catch(Exception ex) {
			ex.printStackTrace();
		}finally {
			if(ps != null) {
				try {
					ps.close();
				}catch(Exception ex) {}
			} // if
			
			if(conn != null) {
				try {
					conn.close();
				}catch(Exception ex) {}
			} // if
		} // finally

		return deleteCount;
	}
}
```

---


>JDBCExam4.java

```java
package kr.or.connect.jdbcexam;

import kr.or.connect.jdbcexam.dao.RoleDao;

public class JDBCExam4 {
	public static void main(String[] args) {
		int roleId = 500;

		RoleDao dao = new RoleDao();
		int deleteCount = dao.deleteRole(roleId);

		System.out.println(deleteCount);
	}
}
```

## - JDBC 수정

>RoleDao.java

```java
package kr.or.connect.jdbcexam.dao;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;

import kr.or.connect.jdbcexam.dto.Role;

public class RoleDao {
	private static String dburl = "jdbc:mysql://localhost:3306/connectdb";
	private static String dbUser = "connectuser";
	private static String dbpasswd = "connect123!@#";
	
	public int updateRole(Role role) {
		int updateCount = 0;
		
		
		Connection conn = null;
		PreparedStatement ps = null;
		
		try {
			Class.forName( "com.mysql.cj.jdbc.Driver" );
			
			conn = DriverManager.getConnection ( dburl, dbUser, dbpasswd );
			
			String sql = "update role set description = ? where role_id = ?";
			
			ps = conn.prepareStatement(sql);
			
			ps.setString(1, role.getDescription());
			ps.setInt(2,  role.getRoleId());
			
			updateCount = ps.executeUpdate();

		}catch(Exception ex) {
			ex.printStackTrace();
		}finally {
			if(ps != null) {
				try {
					ps.close();
				}catch(Exception ex) {}
			} // if
			
			if(conn != null) {
				try {
					conn.close();
				}catch(Exception ex) {}
			} // if
		} // finally
		
		return updateCount;
	}
}

```

---

>JDBCExam5.java

```java
package kr.or.connect.jdbcexam;

import kr.or.connect.jdbcexam.dao.RoleDao;
import kr.or.connect.jdbcexam.dto.Role;

public class JDBCExam5 {
	public static void main(String[] args) {
		int roleId = 501;
		String description = "CEO";
		
		Role role = new Role(roleId, description);
		
		RoleDao dao = new RoleDao();
		int updateCount = dao.updateRole(role);

		System.out.println(updateCount);
	} 
}
```

# 3. API

>Application Programming Interface

`응용 프로그램`에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 `기능을 제어할 수 있게 만든 인터페이스`

- 파일 제어
- 창 제어
- 화상 처리
- 문자 제어

라이브러리를 사용할 때 구현코드를 알지 못해도 `인터페이스만 알면 사용할 수 있음`




## - REST API

> REpresentational State Transfer

다양한 클라이언트들에게 정보를 제공하는 방식을 하나로 `일원화`시키기 위해 
`HTTP프로토콜로 API 제공`

- 네이버에서 블로그에 글을 저장할 수 있는 기능 제공
- 글 목록을 읽어갈 수 있도록 외부에 기능을 제공
- 우체국에서 우편번호를 조회 능을 제공
- 구글에서 구글 지도를 사용할 수 있는 기능 제공



### Mashup

> REST API들을 조합한 어플리케이션

[네이버 API 소개](https://developers.naver.com/products/intro/plan/)

[페이스북의 그래프 API](https://developers.facebook.com/docs/graph-api)

[공공 데이터 포털](https://www.data.go.kr/)

### REST가 지켜야할 스타일

> REST 스타일(제약조건)

-   client-server
-   stateless
-   cache
-   uniform interface
-   layered system
-   code-on-demand (optional)

HTTP프로토콜을 사용한다면 모두 쉽게 구현가능

하지만,  API에서 `uniform interface`의 항목을 지원하기 어려움

-   리소스가 URI로 식별되야 함
-   리소스를 생성,수정,추가하고자 할 때 HTTP메시지에 표현을 해서 전송해야함
-   메시지는 스스로 설명할 수 있어야 함 (Self-descriptive message)
-   애플리케이션의 상태는 Hyperlink를 이용해 전이되야 함(HATEOAS)


세번째 항목 `Self-descriptive message`와  네번째 항목 `HATEOAS`을 API에서 제공하는것은 쉽지 않기 때문에 보통 `Web API(혹은 HTTP API)` 사용

---

## - Web API(혹은 HTTP API)

> REST의 모든 스타일을 구현하지 않음

### Web API 디자인 가이드

-   URI는 정보의 자원을 표현해야 합니다.
-   자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현

### HTTP Method

- **GET**: 리소스 조회
- **POST**: 리소스 생성
- **PUT**: 리소스 수정
- **DELETE**: 리소스 삭제


### HTTP Method로 표현
 
-   GET /members/1 (o)
-   GET /members/get/1 (x)
-   GET /members/add (x)
-   POST /members (o)
-   GET /members/update/1 (x)
-   PUT /members/1 (o)
-   GET /members/del/1 (x)
-   DELETE /members/1 (o)

---

-   슬래시 구분자(/)는 계층을 나타낼 때 사용
-   URI 마지막 문자로 슬래시 구분자(/)를 포함하지 않음
-   하이픈(-)은 URI가독성을 높일 때 사용
-   언더바(_)는 사용하지 않음
-   URI경로는 소문자만 사용
-   RFC 3986(URI 문법 형식)은 URI스키마와 호스트를 제외하고는 대소문자를 구별
-   파일 확장자는 URI에 포함하지 않음
-   Accept Header를 사용


### 상태코드

-   **200**: 클라이언트 요청 정상적으로 수행
-    **201**: 클라이언트의 리소스 생성요청(POST) 성공적으로 수행
-   **400**: 클라이언트 요청이 부적절
-    **401**: 클라이언트가 인증되지 않은 상태에서 보호된 리소스 요청
-    **403**:  클라이언트가 응답하고싶지 않은 리소스를 요청(**400**이나 **404**권고)
-    **405**: 클라이언트가 요청한 리소스에서는 사용불가능한 Method 이용
-    **301**: 클라이언트가 요청한 리소스스에대 한 URL이 변경됨
-    **500**: 서버에 문제가 있음


### Web API 예제



1. 새로운 Maven Project에 생성
2. `Navigator`탭으로 이동
3. `.seetings` > `org.eclipse.wst.common.poject.facet.core.xml` 열기 
4. `jst.web` 버전 `3.1`로 변경
5. 이클립스 재시작
6. `propertices` > `Project Facets` > 'dynamic web module`이 `3.1`로 바뀐것 확인
7. `WEB-INF/web.xml` 삭제
8. pom.xml에 `<failOnMissingWebXml>` 엘리먼트 추가
9. `src/main`에 `java`폴더 생성
10. 다시 `Project Explorer` 탭으로 이동
11. `src/main/java`에 새로운 패키지 생성
12. `src/main/java`에 JDBC에서 사용했던 패키지 `kr.or.connect.jdbcexam.dao`와 `kr.or.connect.jdbcexam.dto` 이클립스 내에서 복사
13. `src/main/java`에 만들었던 패키지 밑에 `RolesServlet`서블릿 생성

> pom.xml
> 

```xml
<?xml version="1.0" encoding="UTF-8"?>

<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>kr.or.connect</groupId>
	<artifactId>webapiexam</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>war</packaging>

	<name>webapiexam Maven Webapp</name>
	<!-- FIXME change it to the project's website -->
	<url>http://www.example.com</url>

	<properties>
	<!-- 3.1로 바꾸었기 때문에 web.xml 파일을 삭제함. 오류가 발생하기 때문에 false로 값을 넣어주자 -->
		<failOnMissingWebXml>false</failOnMissingWebXml>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<maven.compiler.source>1.7</maven.compiler.source>
		<maven.compiler.target>1.7</maven.compiler.target>
	</properties>

	<dependencies>
		<!-- mysql 추가 -->
		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<version>8.0.23</version>
		</dependency>
		<!-- json 라이브러리 databind jackson-core, jackson-annotaion에 의존성이 있다. -->
		<dependency>
			<groupId>com.fasterxml.jackson.core</groupId>
			<artifactId>jackson-databind</artifactId>
			<version>2.9.4</version>
		</dependency>
		<!-- 서블릿 추가 -->
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>javax.servlet-api</artifactId>
			<version>3.1.0</version>
			<scope>provided</scope>
		</dependency>
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.11</version>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<finalName>webapiexam</finalName>
		<pluginManagement><!-- lock down plugins versions to avoid using Maven 
				defaults (may be moved to parent pom) -->
			<plugins>
				<plugin>
					<artifactId>maven-clean-plugin</artifactId>
					<version>3.1.0</version>
				</plugin>
				<!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
				<plugin>
					<artifactId>maven-resources-plugin</artifactId>
					<version>3.0.2</version>
				</plugin>
				<plugin>
					<artifactId>maven-compiler-plugin</artifactId>
					<version>3.8.0</version>
				</plugin>
				<plugin>
					<artifactId>maven-surefire-plugin</artifactId>
					<version>2.22.1</version>
				</plugin>
				<plugin>
					<artifactId>maven-war-plugin</artifactId>
					<version>3.2.2</version>
				</plugin>
				<plugin>
					<artifactId>maven-install-plugin</artifactId>
					<version>2.5.2</version>
				</plugin>
				<plugin>
					<artifactId>maven-deploy-plugin</artifactId>
					<version>2.8.2</version>
				</plugin>
			</plugins>
		</pluginManagement>
	</build>
</project>

```

---

>RolesServlet.java
>

```java
package kr.or.connect.webapiexam.api;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.List;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.fasterxml.jackson.databind.ObjectMapper;

import kr.or.connect.jdbcexam.dao.RoleDao;
import kr.or.connect.jdbcexam.dto.Role;

@WebServlet("/roles")
public class RolesServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;

	public RolesServlet() {
		super();
	}

	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		response.setCharacterEncoding("utf-8"); // 한글처리를 위해 필요
		response.setContentType("application/json"); //json으로 타입지정

		RoleDao dao = new RoleDao(); // kr.or.connect.jdbcexam.dao 밑에 있는 RoleDao클래스

		List<Role> list = dao.getRoles();

		ObjectMapper objectMapper = new ObjectMapper(); //json문자열을 객체로 바꿈
		String json = objectMapper.writeValueAsString(list); //list가 json문자로 바꿈

		PrintWriter out = response.getWriter();
		out.println(json);
		out.close();
	}

}
```




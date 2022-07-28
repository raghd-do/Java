# Getting Started
- [Installation](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#installation-for-windows)
- [For Each Project setup](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#for-each-project-setup)
  - [pom.xml](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#pomxml)
  - [application.properties](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#applicationproperties)
  - [jsp files](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#filejsp)
- [Spring Data JPA](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#spring-data-jpa)
  - [setup](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#dependencies-and-set-up)
## Installation for Windows
### Maven
1. Download the latest version of Maven from this: http://maven.apache.org/download.cgi
2. Follow the download instructions depending on your laptop/computer's operating system. For windows, download from the Binary zip archive
3. The installation of Apache Maven is a simple process of extracting the archive and adding the bin folder with the mvn command to the PATH.
  - Make sure that JAVA_HOME environment variable is set and points to the JDK installing folder.
  - Unzip the downloaded maven zip.
  - Add the bin directory of the created directory apache-maven-3.5.0 to the user PATH environment variable
  - Confirm with `mvn --version` in a new shell.
  - To check your enviroment variables:
```
echo %JAVA_HOME% 
C:\Program Files\Java\jdk1.7.0_51
```
### Spring Tool Suite (STS)
Download the latest version of STS ([Spring Tool Suite](https://spring.io/tools))  and install it on your system.

If it is your first time launching STS, it will ask you where you want to save your projects. Choose the path you want them saved in, and that's it!

# For Each Project setup
## pom.xml
tomcat
```html
<dependency>
  <groupId>org.apache.tomcat.embed</groupId>
  <artifactId>tomcat-embed-jasper</artifactId>
</dependency>
```
jstl
```html
<dependency>
  <groupId>javax.servlet</groupId>
  <artifactId>jstl</artifactId>
</dependency>
```
webjars
```html
<dependency>
  <groupId>org.webjars</groupId>
  <artifactId>webjars-locator</artifactId>
  <version>0.30</version>
</dependency>
```
run time (to make the code Live and auto changed)
```html
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
    <optional>true</optional>
</dependency>
```
### for Static files
Bootstrap
```html
<dependency>
  <groupId>org.webjars</groupId>
  <artifactId>bootstrap</artifactId>
  <version>5.0.1</version>
</dependency>
```
JQuery
```html
<dependency>
  <groupId>org.webjars</groupId>
  <artifactId>jquery</artifactId>
  <version>3.6.0</version>
</dependency>
```
## application.properties
WEB-INF could be named any thing BUT make sure to match the file that you will be creating under: `src/main/webapp`
```
spring.mvc.view.prefix=/WEB-INF/

// to connect to our Data source
spring.datasource.url=jdbc:mysql://localhost:3306/<<YOUR_SCHEMA>>
spring.datasource.username=<<dbuser>>
spring.datasource.password=<<dbpassword>>
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.jpa.hibernate.ddl-auto=update
```

## file.jsp
### Links
core tag library link 
```html
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
```
Bootstrab link
```html
<!-- for Bootstrap CSS -->
<link rel="stylesheet" href="/webjars/bootstrap/css/bootstrap.min.css" />
```
CSS link
```html
<link rel="stylesheet" type="text/css" href="#">
```
JS link
```html
<script type="text/javascript" src="#"></script>
```
### Java standard tags library
display
```html
<c:out value="${ name }" />
```
loop
```html
<c:forEach var="fruit" items="${ fruits }">
  <tr>
    <td><c:out value="${ fruit.name }"/></td>
    <td><c:out value="${ fruit.price }"/></td>
  </tr>
</c:forEach>
```
format Date (takes Date object as value)
```html
<!-- taglib -->
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt"%>
  
<!-- Use -->
<fmt:formatDate type="date" dateStyle = "long" pattern="E ', the ' d ' of ' M', ' y" value="${ date }"/>
<fmt:formatDate type="time" timeStyle = "short" value="${ date }"/>
```
ternary operator
```html
<p style="${log.contains('lost') ? 'color: red':'color:green'}">
  <c:out value="${log}" />
</p>
```
if condition
```html
<c:if test="${ condition }"/></c:if>
```
if else statement
```html
<c:choose>
   <c:when test="${..}">...</c:when> <!-- if condition -->
   <c:when test="${..}">...</c:when> <!-- else if condition -->
   <c:otherwise>...</c:otherwise>    <!-- else condition -->
</c:choose>
```
redirect
```html
<c:redirect url="/home"/>
```
# Spring Data JPA
## Dependencies and Set-up:
### when creating new project
  - DevTools
  - JPA
  - MySQL
  - Web
### or in pom.xml
```html
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```
## MySQL Server Set-up
#### Note: Make sure your MySQL server is running.
in the taskbar search for `Services` click on any shown item the press `m` to filter the item. sesrch for `MySQL80` right click on it then `start` to start thr service, or `stop` to stop it when you done.

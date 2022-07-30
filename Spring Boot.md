# Getting Started
1. [For Each Project setup](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#for-each-project-setup)
	- [pom.xml](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#pomxml)
	- [application.properties](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#applicationproperties)
	- [jsp files](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#filejsp)
	- [Java Standard Tags Library](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#java-standard-tags-library---more) 
2. [Routing](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#routing)
	- [GET](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#get)
	- [POST](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#post)
	- [PUT](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#put---for-updating)
	- [DELETE](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#delete---for-deleting)
3. [Data Storages](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#data-storages)
	- [View Model](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#view-model)
	- [HttpSession](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#httpsession)
	- [Flash Data](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#flash-data)
4. [Spring Data JPA](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#spring-data-jpa)
	- [Entity](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#entity---class)
	- [Repository](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#repository---interface)
	- [Service](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#service---class)
	- [Controller](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#controller---class)
---
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
validations (for the @Entity class attributes)
```html
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
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
```
to enable hidden input tag to specify for the request methods to be PUT or DELETE
```
spring.mvc.hiddenmethod.filter.enabled=true
```
to connect to our Data source
```
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
form tag library link
```html
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>
```
to allow us to render the view on a PUT request
```html
<%@ page isErrorPage="true" %>
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
### Java standard tags library - [more](https://www.baeldung.com/jstl)
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
#### Form tags
##### Form
```html
<form:form action="/books" method="post" modelAttribute="book">
```
##### Label
```html
<form:label path="title">Title</form:label>
```
##### Input
```html
<form:input path="title" type="text" cssClass="form-control" cssErrorClass="form-control is-invalid"/>
```
include `step="any"` attribute to allow frections on the input number
```html
 <form:input path="numberOfPages" type="number" cssClass="form-control" cssErrorClass="form-control is-invalid"/>
```
##### Textarea
```html
<form:textarea path="description"/>
```
##### Errors
rendering error for one
```html
<form:errors path="language" class="invalid-feedback"/>
```
rendering error for all
```html
<form:errors path="book.*" element="div" class="invalid-feedback"/>
```
# Routing
## GET
```java
@RequestMapping(value="/home", method=RequestMethod.GET) // general way
@RequestMapping("/home") // by defult --> Get
@GetMapping("/home")
```
## POST
```java
@RequestMapping(value="/login", method=RequestMethod.POST)
@PostMapping("/logint")
```
## PUT - for updating
```java
@RequestMapping(value="/update/{id}", method=RequestMethod.PUT)
```
## DELETE - for deleting
```java
@RequestMapping(value="/delete/{id}", method=RequestMethod.DELETE)
```
## Query Parameters
url: `localhost:8080/?name=Cat`
```java
@RequestMapping("/")
public String index(@RequestParam("name") String name) {
    // TODO
}
```
url: `localhost:8080/?name=Cat&age=3`
```java
@RequestMapping("/")
public String index(
    @RequestParam(value="name" required=false) String name, // required by defult = true
    @RequestParam(value="age" required=false, defaultValue = "1") Integer age
    ) {
    // TODO
}
```
## Form Submission
```java
@PostMapping("/login")
public String login(
	@RequestParam(value="email") String email,
  @RequestParam(value="password") String password
  ) {  
  // CODE TO PROCESS FORM ie. check email and password  	
  return "redirect:/home"; // redirect usually used with session
}
```
## Path Variabl
```java
@RequestMapping("/book/{id}")
public String showBook(@PathVariable("id") Long id) {
    // TODO
}
```
# Data Storages
## View Model
### getting data into the jsp file from our controller
```java
public String index(Model model) {
    model.addAttribute("name", "Raghad");
    return "index.jsp";
}
```
then we call it in jsp file
```html
<body>
    <p>
        <c:out value="${name}"/>
    </p>
</body>
```
## HttpSession
### to persist any information across requests
will create it if doesn't exist OR update it if it does
```java
public String index(HttpSession session) {
    session.setAttribute("count", 0);
    return "index.jsp";
}
```
get the session value
```java
public String showCount(HttpSession session, Model model) {
  Integer currentCount = (Integer) session.getAttribute("count");
  model.addAttribute("countToShow", currentCount);
  return "showCount.jsp";
}
```
check if it is null
```java
  // If the count is not already in session
if (session.getAttribute("count") == null) {
    // initialize the count in session
    session.setAttribute("count", 0);
}
else {
    // increment the count by 1
    session.setAttribute("count", (Integer) session.getAttribute("count") + 1);
}
return "index.jsp";
```
## Flash Data
is data that only persists across the next request.
This sort of session data is very useful for things such as `error messages`, `success notification`, or anything else that you would want to show a user only immediately following their request
```java
@RequestMapping("/createError")
public String flashMessages(RedirectAttributes redirectAttributes) {
  redirectAttributes.addFlashAttribute("error", "A test error!");
  return "redirect:/";
}
```
## MySQl
to persist data [MySQL](https://dev.mysql.com/downloads/windows/installer/8.0.html)
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
### MySQL Server Set-up
#### Note: Make sure your MySQL server is running.
in the taskbar search for `Services` then click to open it, click on any shown item then press `m` to filter the item. sesrch for `MySQL80` right click on it then `start` to start thr service, or `stop` to stop it when you done.
### Project Set-up
#### application.properties
use `?serverTimezone=UTC` part when you have `The server time zone value 'PDT' is unrecognized or...` Error
```
spring.datasource.url=jdbc:mysql://localhost:3306/<<YOUR_SCHEMA>>?serverTimezone=UTC
spring.datasource.username=<<dbuser>>
spring.datasource.password=<<dbpassword>>
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.jpa.hibernate.ddl-auto=update
```
when facing a `Loading class com.mysql.jdbc.Driver'. This is deprecated.` Error
You may safely remove this setting
```
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
```
## Entity - class
### Creation
```Java
@Entity
@Table(name="books")
public class Book {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    // Constructor
    // Getters & Setters
}
```
### Validation Annotations
sets this as the primary key
```Java
@Id
```
sets this as an auto-incrementing value
```Java
@GeneratedValue(strategy = GenerationType.IDENTITY)
```
adds validation that the column must be in the specified range
```Java
@Size(min = 5, max = 200)
```
adds validation that the column must be at least the specified value
```Java
@Min(100)
```
adds validation that the column must be null
```Java
@NotNull
```
runs the method right before the object is created
```Java
@PrePersist
protected void onCreate(){
    this.createdAt = new Date();
}
```
runs a method when the object is modified
```Java
@PreUpdate
protected void onUpdate(){
    this.updatedAt = new Date();
}
```
This will not allow the createdAt column to be updated after creation
```Java
@Column(updatable=false)
```
set the Date value in a specific format pattern
```Java
@DateTimeFormat(pattern="yyyy-MM-dd")
```
### Custom Error Messages
adding a message to the arguments in the corresponding validation annotation
```java
@Size(min = 3, max = 40, message="Language must be at least 3 characters.")
```
```java
@Min(value=100, message="Must be at least 100 pages.")
```
## Repository - interface
Data repositories are where we gain access to all our data
### Creation
this will automatically allow us to create, read, update, and destroy our books
it will automatically build queries from method names in your interface
```Java
@Repository
public interface BookRepository extends CrudRepository<Book, Long>{
...
}
```
### Methods - [more](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/CrudRepository.html) | [examples](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods.query-creation) | [query keywords](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repository-query-keywords) | [derived query example](https://www.baeldung.com/spring-data-derived-queries)
retrieves all - (must be declared)
```Java
List<Book> findAll();
```
save a given entity
```Java
bookRepository.save(b)
```
filtering query
```Java
List<Book> findByDescriptionContaining(String search);
```
## Service - class
Services are the business logic of our application
### Creation
```java
@Service
public class BookService {
    private final BookRepository bookRepository;

    public BookService(BookRepository bookRepository) { // independence injection
      this.bookRepository = bookRepository;
    }
// Methods
}
```
### OR
```java
@Service
public class BookService {
    @Autowired
    BookRepository bookRepository;
// Methods
}
```
### Methods
retrieve all
```java
public List<Book> allBooks() {
  return bookRepository.findAll();
}
```
Create a book
```java
public Book createBook(Book b) {
  return bookRepository.save(b);
}
```
retrieve a book by id
```java
public Book findBook(Long id){
  Optional<Book> optionalBook = bookRepository.findById(id);
  if(optionalBook.isPresent()) {
    return optionalBook.get();
  } else {
    return null;			
  }
}
```
update a spisific book
```java
public Book updateBook(Long id, String title, String desc, String lang, Integer numOfPages) {
  Optional<Book> optionalBook = bookRepository.findById(id);
  if(optionalBook.isPresent()) {
    Book book = optionalBook.get();
    book.setTitle(title);
    book.setDescription(desc);
    book.setLanguage(lang);
    book.setNumberOfPages(numOfPages);
    bookRepository.save(book);
    return book;
  }
  return null;
}
```
delete a spisific book
```java
public void deleteBook(Long id) {
  bookRepository.deleteById(id);
}
```
## Controller - class
our API to execute the CRUD operations
### Tools to test the API
[PostMan](https://www.getpostman.com/apps)
### Creation
```java
@RestController // for API requests, OR
@Controller // render real pages
public class BooksController {
    private final BookService bookService;
    public BooksApi(BookService bookService){
        this.bookService = bookService;
    }
    // Methods
}
```
#### OR
```java
@Controller
public class BooksController {
    @Autowired
    BookService bookService;
    // Methods
}
```
---
### CRUD Methods
#### retriving all books
##### API
```java
@RequestMapping("/api/books")
public List<Book> index() {
    return bookService.allBooks();
}
```
##### JSP Views
```java
public String index(Model model) {
	List<Book> books = bookService.allBooks();

	model.addAttribute("books", books);
	return "index.jsp";
}
```
#### C - creating a book
##### API
```java
@RequestMapping(value="/api/books", method=RequestMethod.POST)
public Book create(
    @RequestParam(value="title") String title,
    @RequestParam(value="description") String desc,
    @RequestParam(value="language") String lang,
    @RequestParam(value="pages") Integer numOfPages
    ) {
        Book book = new Book(title, desc, lang, numOfPages);
        return bookService.createBook(book);
}
```
##### JSP Views
Add `@ModelAttribute` annotation and associated syntax to your render route, to bind an empty Book object to the JSP form to capture the user input.

`@Valid` annotation to check if the submitted object passes validation
`BindingResult` to see if the object passed validation. **This must come immediately after the `@Valid` parameter**
Once we have the `BindingResult` we can check if there were any errors, and then reload our form with errors if there are any.
```java
// Add Form
@GetMapping("/books/new")
public String newBook(@ModelAttribute("book") Book book) { // Add empty Book object to bind it for the form
	return "/books/new.jsp";
}
// Add Process
@PostMapping("/books")
public String create(@Valid @ModelAttribute("book") Book book, BindingResult result) {
	if (result.hasErrors()) {
	    return "/books/new.jsp";
	} else {
	    bookService.createBook(book);
	    return "redirect:/books";
	}
}
```
jsp
```html
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>
<!-- part removed -->
<form:form action="/books" method="post" modelAttribute="book">
```
### R - retriving a specific book
##### API
```java
@RequestMapping("/api/books/{id}")
public Book show(@PathVariable("id") Long id) {
    Book book = bookService.findBook(id);
    return book;
}
```
##### JSP Views
```java
@RequestMapping("/books/{id}")
public String show(Model model, @PathVariable("id") Long id) {
	Book book = bookService.findBook(id);

	model.addAttribute("book", book);
	return "show.jsp";
}
```
### U - updating a specific book
##### API
```java
@RequestMapping(value="/api/books/{id}", method=RequestMethod.PUT)
public Book update(
    @PathVariable("id") Long id,
    @RequestParam(value="title") String title, 
    @RequestParam(value="description") String desc, 
    @RequestParam(value="language") String lang,
    @RequestParam(value="pages") Integer numOfPages) {
    Book book = bookService.updateBook(id, title, desc, lang, numOfPages);
    return book;
}
```
##### JSP Views
```java
// Edit form
@GetMapping("/books/{id}/edit")
public String edit(@PathVariable("id") Long id, Model model) {
	Book book = bookService.findBook(id);
	model.addAttribute("book", book);
	return "edit.jsp";
}

// Edit Process
@RequestMapping(value="/books/{id}", method=RequestMethod.PUT)
public String update(@Valid @ModelAttribute("book") Book book, BindingResult result, @PathVariable("id") Long id) {
	if (result.hasErrors()) {
		return "edit.jsp";
	} else {
		bookService.updateBook(id, book);
		return "redirect:/books";
	}
}
```
### D - deleting a specific book
##### API
```java
@RequestMapping(value="/api/books/{id}", method=RequestMethod.DELETE)
public void destroy(@PathVariable("id") Long id) {
    bookService.deleteBook(id);
}
```
##### JSP Views
```java

```

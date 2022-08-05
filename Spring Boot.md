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
      - [Login & Registration page](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#registration--log-in-page)
5. [Relationships](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#relationships)
    - [1:1](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#11)
    - [1:n](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#1n)
    - [m:n](https://github.com/raghd-do/Java/blob/main/Spring%20Boot.md#mn)
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
for using BCrypt
```html
<dependency>
    <groupId>org.mindrot</groupId>
    <artifactId>jbcrypt</artifactId>
    <version>0.4</version>
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
Where are jsp files? HERE!
WEB-INF could be named any thing BUT make sure to match the file that you will be creating under: `src/main/webapp` 
```
spring.mvc.view.prefix=/WEB-INF/
```
to enable hidden input tag to specify for the request methods to be PUT or DELETE
```
spring.mvc.hiddenmethod.filter.enabled=true
```
to connect to our Data source (Data Persistence)
```
spring.datasource.url=jdbc:mysql://localhost:3306/<<YOUR_SCHEMA>>
spring.datasource.username=<<dbuser>>
spring.datasource.password=<<dbpassword>>
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
spring.jpa.hibernate.ddl-auto=update
```

## file.jsp
### Links
```html
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<!-- c:out ; c:forEach etc. --> 
<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
<!-- Formatting (dates) --> 
<%@taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt"%>
<!-- form:form -->
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form"%>
<!-- for rendering errors on PUT routes -->
<%@ page isErrorPage="true" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Tacos</title>
<link rel="stylesheet" href="/webjars/bootstrap/css/bootstrap.min.css">
<link rel="stylesheet" href="/css/main.css"> <!-- change to match your file/naming structure -->
<script src="/webjars/jquery/jquery.min.js"></script>
<script src="/webjars/bootstrap/js/bootstrap.min.js"></script>
</head>
<body>
   
</body>
</html>
```
core tag library link 
```html
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
```
form tag library link
```html
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>
```
Formatting (dates)
```
<%@taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt"%>
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
JQuery link
```html
<script src="/webjars/jquery/jquery.min.js"></script>
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
#### Form tags [more](https://www.baeldung.com/spring-mvc-form-tags)
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
@PutMApping("/update/{id}")
```
## DELETE - for deleting
```java
@RequestMapping(value="/delete/{id}", method=RequestMethod.DELETE)
@DeleteMapping("/delete/{id}")
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
    @RequestParam(value="name", required=false) String name, // required by defult = true
    @RequestParam(value="age", required=false, defaultValue = "1") Integer age
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
`created at` & `updated at` columns
```java
// This will not allow the createdAt column to be updated after creation
@Column(updatable = false)
// set the Date value in a specific format pattern
@DateTimeFormat(pattern = "yyyy-MM-dd")
private Date createdAt;
@DateTimeFormat(pattern = "yyyy-MM-dd")
private Date updatedAt;

// runs the method right before the object is created
@PrePersist
protected void onCreate() {
  this.createdAt = new Date();
}

// runs a method when the object is modified
@PreUpdate
protected void onUpdate() {
  this.updatedAt = new Date();
}
```
#### Custom Error Messages
adding a message to the arguments in the corresponding validation annotation
```java
@Size(min = 3, max = 40, message="Language must be at least 3 characters.")
```
```java
@Min(value=100, message="Must be at least 100 pages.")
```
### Regesration Model -- Entit
```java
@Entity
@Table(name="users")
public class User {
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id;

  @NotEmpty(message="Username is required!")
  @Size(min=3, max=30, message="Username must be between 3 and 30 characters")
  private String userName;

  @NotEmpty(message="Email is required!")
  @Email(message="Please enter a valid email!")
  private String email;

  @NotEmpty(message="Password is required!")
  @Size(min=8, max=128, message="Password must be between 8 and 128 characters")
  private String password;

  @Transient // wont be stored in the database
  @NotEmpty(message="Confirm Password is required!")
  @Size(min=8, max=128, message="Confirm Password must be between 8 and 128 characters")
  private String confirm;
  // ...
}
```
### Login Model -- not Entity
```java
public class LoginUser {
    
  @NotEmpty(message="Email is required!")
  @Email(message="Please enter a valid email!")
  private String email;
  
  @NotEmpty(message="Password is required!")
  @Size(min=8, max=128, message="Password must be between 8 and 128 characters")
  private String password;
  
  public LoginUser() {}
  
  // TODO - getters and setters
    
}
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
### Methods - [more](https://docs.spring.io/spring-data/commons/docs/current/api/org/springframework/data/repository/CrudRepository.html) | [search examples](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods.query-creation) | [query keywords](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repository-query-keywords) | [derived query example](https://www.baeldung.com/spring-data-derived-queries)
retrieves all - (must be declared)
```Java
List<Book> findAll();
```
save a given entity
```Java
bookRepository.save(b)
```
for registeration & login use
```java
Optional<User> findByEmail(String email);
```
#### Filtering & Searching querys
```Java
List<Book> findByDescriptionContaining(String search);
```
search for songs made by the brovided artist - ignore case + contain
```java
List<Song> findByArtistContaining(String artist);
```
find the list of top 10 in descending order
```java
List<Playlist> findTop10ByOrderByRatingDesc();
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
#### retrieve all
```java
public List<Book> allBooks() {
  return bookRepository.findAll();
}
```
#### Create a book
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
#### update a spisific book
##### API
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
##### JSP Views
```java
public Book updateBook(Long id, Book ubook) {
  Optional<Book> optionalBook = bookRepository.findById(id);
  if(optionalBook.isPresent()) {
    Book book = optionalBook.get();
    book.setTitle(ubook.getTitle());
    book.setDescription(ubook.getDescription());
    book.setLanguage(ubook.getLanguage());
    book.setNumberOfPages(ubook.getNumberOfPages());
    bookRepository.save(book);
    return book;
  }
  return null;
}
```
#### delete a spisific book
```java
public void deleteBook(Long id) {
  bookRepository.deleteById(id);
}
```
#### Search
```java
public List<Song> findByArtist(String artist) {
  return songRepository.findByArtistContaining(artist);
}
```
### Registration method
```java
public User register(User newUser, BindingResult result) {
    if(userRepo.findByEmail(newUser.getEmail()).isPresent()) {
        result.rejectValue("email", "Unique", "This email is already in use!");
    }
    if(!newUser.getPassword().equals(newUser.getConfirm())) {
        result.rejectValue("confirm", "Matches", "The Confirm Password must match Password!");
    } else {
        String hashed = BCrypt.hashpw(newUser.getPassword(), BCrypt.gensalt());
        newUser.setPassword(hashed);
        return userRepo.save(newUser);
    }
    return null;
}
```
### Login method
```java
public User login(LoginUser newLogin, BindingResult result) {
    Optional<User> potentialUser = userRepo.findByEmail(newLogin.getEmail());
    if(!potentialUser.isPresent()) {
        result.rejectValue("email", "Unique", "Unknown email!");
        return null;
    }
    User user = potentialUser.get();
    if(!BCrypt.checkpw(newLogin.getPassword(), user.getPassword())) {
        result.rejectValue("password", "Matches", "Invalid Password!");
        return null;
    }
    return user;
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
// alternative way to do it is:
// model.addAttribute("book", new Book());
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
#### R - retriving a specific book
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
#### U - updating a specific book
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
jsp
`_method` to tell the http request the real method of the form
```html
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>
<!-- part removed -->
<form:form action="/books/${ book.id }" method="post" modelAttribute="book">
  <input type="hidden" name="_method" value="put"/>
```
#### D - deleting a specific book
##### API
```java
@RequestMapping(value="/api/books/{id}", method=RequestMethod.DELETE)
public void destroy(@PathVariable("id") Long id) {
    bookService.deleteBook(id);
}
```
##### JSP Views
```java
@RequestMapping(value="/books/{id}", method=RequestMethod.DELETE)
public String destroy(@PathVariable("id") Long id) {
    bookService.deleteBook(id);
    return "redirect:/books";
}
```
jsp
```html
<form action="/books/${book.id}" method="post">
  <input type="hidden" name="_method" value="delete">
  <button type="submit" class="btn btn-danger">Delete</button>
</form>
```
#### S - Search
```java
@GetMapping("/search")
public String search(@RequestParam("artist") String artist, Model model) {
  List<Song> songs = songService.findByArtist(artist);
  model.addAttribute("songs", songs);
  return "search.jsp";
}
```
jsp
```html
<form class="d-flex" role="search">
  <input name="artist" class="form-control me-2" type="search" placeholder="Search Artist" aria-label="Search">
  <button class="btn btn-outline-success" type="submit">Search</button>
</form>
```
### Registration & Login
#### GET form page
```java
@GetMapping("/")
public String createUserView(Model model) {
  if(!model.containsAttribute("newUser")) {
    model.addAttribute("newUser", new User());
  }

  if(!model.containsAttribute("newLogin")) {
    model.addAttribute("newLogin", new LoginUser());
  }
  return "index.jsp";
}
```
#### POST Registration
```java
@PostMapping("/register")
public String createUserAction(
    @Valid @ModelAttribute("newUser") User newUser,
    BindingResult result,
    RedirectAttributes redirectAttributes,
    HttpSession session
    ) {
  if(result.hasErrors()) {
    redirectAttributes.addFlashAttribute("newUser", newUser);
    redirectAttributes.addFlashAttribute("org.springframework.validation.BindingResult.newUser", result);
    return "redirect:/";
  }
  User user = userService.register(newUser, result);
  if(user == null) {
    redirectAttributes.addFlashAttribute("newUser", newUser);
    redirectAttributes.addFlashAttribute("org.springframework.validation.BindingResult.newUser", result);
    return "redirect:/";
  } else {
    session.setAttribute("user_id", user.getId());
    return "redirect:/loginChecker";
  }
}
```
#### POST Login
```java
@PostMapping("/login")
public String loginUser(
    @Valid @ModelAttribute("newLogin") LoginUser newLogin,
    BindingResult result,
    RedirectAttributes redirectAttributes,
    HttpSession session
    ) {
  if(result.hasErrors()) {
    redirectAttributes.addFlashAttribute("newLogin", newLogin);
    redirectAttributes.addFlashAttribute("org.springframework.validation.BindingResult.newLogin", result);
    return "redirect:/";
  }
  
  User user = userService.login(newLogin);
  if(user == null) {
    result.rejectValue("email", "invalid", "Invalid email or password.");
    redirectAttributes.addFlashAttribute("newLogin", newLogin);
    redirectAttributes.addFlashAttribute("org.springframework.validation.BindingResult.newLogin", result);
    return "redirect:/";
  } else {
    session.setAttribute("user_id", user.getId());
    return "redirect:/loginChecker";
  }
}
```
#### Registration & Log in page
```html
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>
    
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
<%@taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt"%>
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form"%>
<%@ page isErrorPage="true" %>

<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Login & Registration</title>
<link rel="stylesheet" href="/webjars/bootstrap/css/bootstrap.min.css">
<script src="/webjars/bootstrap/js/bootstrap.min.js"></script>
</head>
<body>
	<div class="container mt-5">
		<h1 class="text-danger">Welcome!</h1>
		<p class="text-dark h5">Join our growing community.</p>
		<br>
		<div class="row">
			<div class="col">
				<h2 class="text-dark">Register</h2>
			    <form:form action="/register" method="post" modelAttribute="newUser">
			        <div class="form-group mb-3">
			            <label>User Name:</label>
			            <form:input path="userName" class="form-control" />
			            <form:errors path="userName" class="text-danger" />
			        </div>
			        
			        <div class="form-group mb-3">
			            <label>Email:</label>
			            <form:input path="email" class="form-control" />
			            <form:errors path="email" class="text-danger" />
			        </div>
			        
			        <div class="form-group mb-3">
			            <label>Password:</label>
			            <form:password path="password" class="form-control" />
			            <form:errors path="password" class="text-danger" />
			        </div>
			        
			        <div class="form-group mb-3">
			            <label>Confirm Password:</label>
			            <form:password path="confirm" class="form-control" />
			            <form:errors path="confirm" class="text-danger" />
			        </div>
			        
        			<input type="submit" value="Register" class="btn btn-primary" />
				</form:form>
   			</div>
   			
    		<div class="col">
    			<h2 class="text-dark">Log in</h2>
    			<form:form action="/login" method="post" modelAttribute="newLogin">
			        <div class="form-group mb-3">
			            <label>Email:</label>
			            <form:input path="email" class="form-control" />
			            <form:errors path="email" class="text-danger" />
			        </div>
			        
			        <div class="form-group mb-3">
			            <label>Password:</label>
			            <form:password path="password" class="form-control" />
			            <form:errors path="password" class="text-danger" />
			        </div>
			        
        			<input type="submit" value="Login" class="btn btn-success" />
    			</form:form>
			</div>
		</div>
	</div>
</body>
</html>
```
### Extra TIP for Validation
when a user submiting unvalid form data
redirect him to the same page with `user input` and `error messages` while mentaning the other page data in loade

for the `book` at the end of `org.springframework.validation.BindingResult.book` must match the `@ModelAttribute("book")` key
#### C - Creating
```java
//	Add Form
@RequestMapping("/new")
public String newBook(Model model) {
  if (!model.containsAttribute("book")) { // to check if there is no user input before it will initialize one
    model.addAttribute("book", new Book());
  }
  return "new.jsp";
}

//	Adding Process
@PostMapping("/new")
public String newBook(@Valid @ModelAttribute("book") Book book, BindingResult result, RedirectAttributes redirect) {
  if (result.hasErrors()) {
    redirect.addFlashAttribute("book", book); // to redirect user inputed data
    redirect.addFlashAttribute("org.springframework.validation.BindingResult.book", result); // to redirect user error messages
    return "redirect:/books/new";
  } else {
    bookService.createBook(book);
    return "redirect:/books";
  }
}
```
#### U - Updating
```java
//	Edit form
@GetMapping("/{id}/edit")
public String edit(@PathVariable("id") Long id, Model model) {
  if(!model.containsAttribute("book")) {
    Book book = bookService.findBook(id);
    model.addAttribute("book", book);			
  }
  model.addAttriput("bookId", id); // when redirecting after an error, the book object will be an object from a form not a database so it doesn't have the ID nor the createdAt or updatedAt.
  return "edit.jsp";
}

//	Edit Process
@RequestMapping(value="/{id}", method=RequestMethod.PUT)
public String update(
  @Valid @ModelAttribute("book") Book book,
  BindingResult result,
  @PathVariable("id") Long id,
  RedirectAttributes redirect
  ) {
  if (result.hasErrors()) {
    redirect.addFlashAttribute("book", book);
    redirect.addFlashAttribute("org.springframework.validation.BindingResult.book", result);
    return "redirect:/books/{id}/edit";
  } else {
    bookService.updateBook(id, book);
    return "redirect:/books";
  }
}
```
# Relationships
## 1:1
### Entity
#### Entity 1
`mappedBy="person"` It represents the field that owns the relationship. This element is only specified on the inverse (non-owning) side **you don't need a license to create a person, but you do need a person to create a license**!
`fetch=FetchType.LAZY`
- LAZY: The association is fetched when needed.
- EAGER: The association is fetched immediately.
```java
@Entity
@Table(name="persons")
public class Person {
  // ...
  @OneToOne(mappedBy="person", cascade=CascadeType.ALL, fetch=FetchType.LAZY)
  private License license;
  // ...
}
```
#### Entity 2
`name="person_id"` Defines mapping for composite foreign keys
```java
@Entity
@Table(name="licenses")
public class License {
  // ...
  @OneToOne(fetch=FetchType.LAZY)
  @JoinColumn(name="person_id")
  private Person person; // from here we generate the (mappedBy="person") in Person class the names must be matched
  // ...
}
```
### JSP form
#### Form 1
```html
```
#### Form 2
```html
<!--- inside the form:form --->
<form:select path="person">
    <c:forEach var="onePerson" items="${persons}">
        <!--- Each option VALUE is the id of the person --->
        <form:option value="${onePerson.id}" path="person">
        <!--- This is what shows to the user as the option --->
            <c:out value="${onePerson.firstName}"/>
            <c:out value="${onePerson.lastName}">
        </form:option>
    </c:forEach>
</form:select>
```
### POST route
```java
@PostMapping("/licenses")
public String licenses(@Valid @ModelAttribute("license") License license) {
    // error handling with binding result omitted    
    licenseService.create(license); // Already has the person!
        
    return "redirect:/persons";
}
```
---
## 1:n
### Entity
#### Entity 1
One `Dojo` To Many `Ninjas` - (`List<Ninja>`)
```java
@Entity
@Table(name="dojos")
public class Dojo {
  // ...
  @OneToMany(mappedBy="dojo", fetch = FetchType.LAZY)
  private List<Ninja> ninjas;
  // ...
}
```
#### Entity 2
Many `Ninjas` To One `Dojo`
```java
@Entity
@Table(name="ninjas")
public class Ninja {
  // ...
  @ManyToOne(fetch = FetchType.LAZY)
  @JoinColumn(name="dojo_id")
  private Dojo dojo;
  // ...
}
```
### JSP form
#### Form 1
```html
<c:forEach var="ninja" items="${ dojo.ninjas }">
  <tr>
    <td><c:out value="${ ninja.firstName }"/></td>
    <td><c:out value="${ ninja.lastName }"/></td>
    <td><c:out value="${ ninja.age }"/></td>
  </tr>		
</c:forEach>
```
#### Form 2
```html
<!--- inside the form:form --->
<form:select path="dojo">
    <c:forEach var="dojo" items="${dojos}">
        <form:option value="${dojo.id}" path="dojo">
            <c:out value="${dojo.location}"/>
        </form:option>
    </c:forEach>
</form:select>
```
### POST route
```java
@PostMapping("/ninjas")
public String ninjas(@Valid @ModelAttribute("ninja") Ninja ninja) {
    // error handling with binding result omitted    
    ninjaService.create(ninja); // it will link the dojo automaticly
        
    return "redirect:/dojos";
}
```
---
## m:n
### Entity
#### Entity 1
```java
```
#### Entity 2
```java
```
### JSP form
#### Form 1
```html
```
#### Form 2
```html
```
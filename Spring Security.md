# Spring Security
### pom.xml
```html
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```
Once we have a database connection, we can check if Spring Security is working correctly. Start your application and navigate to the root route. If you have installed all dependencies, you should see a prompt for a username and password without even writing any code!

By default, Spring Security protects any route in your application. If you would like to log in, the default username is user and the password can be found in your console. Note, this password will be different on every server restart.

## Models
### User
```Java
@Entity
@Table(name="users")
public class User {
    // ...
    @ManyToMany(fetch = FetchType.EAGER)
    @JoinTable(
        name = "users_roles", 
        joinColumns = @JoinColumn(name = "user_id"), 
        inverseJoinColumns = @JoinColumn(name = "role_id"))
    private List<Role> roles;
    // ...
}
```
### Role
```Java
@Entity
@Table(name="roles")
public class Role {
    // ...
    private String name; // role name

    @ManyToMany(mappedBy = "roles")
    private List<User> users;
    // ...
}
```
Restart your application to create the tables in our database. Then, in your roles table, insert two rows: the first row with the value of `user` for the name column and the second with `admin`
```SQL
INSERT INTO `roles` (name) VALUES ('ROLE_USER');
INSERT INTO `roles` (name) VALUES ('ROLE_ADMIN');
```
Our `roles` table will be used to grant users permission to certain actions in our application. It is important to have the `ROLE_` prefix. This is how Spring Security will authorize clients in the application.
## Repositories
### User
```java
@Repository
public interface UserRepository extends CrudRepository<User, Long> {
    User findByUsername(String username);
}
```
### Role
```java
@Repository
public interface RoleRepository extends CrudRepository<Role, Long> {
}
```
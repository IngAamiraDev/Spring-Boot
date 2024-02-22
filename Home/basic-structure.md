# Basic Structure in Spring Boot

## Folder Structure
```bash
/name-project
├── src
│   ├── main
│   │   ├── java
│   │   │   ├── com.comany
│   │   │   │   ├── controller
│   │   │   │   ├── exception
│   │   │   │   ├── model
│   │   │   │   ├── repository
│   │   │   │   ├── service
│   │   ├── resources
│   │   │   ├── application.properties
│   ├── test
├── .gitignore
├── README.md
```

## Overview of Key Components in a Spring Boot Application

### Controller:
In Spring Boot, a controller is a class annotated with `@Controller` or `@RestController` that handles incoming HTTP requests and returns appropriate HTTP responses. These classes contain methods annotated with `@RequestMapping`, `@GetMapping`, `@PostMapping`, etc., which map specific HTTP endpoints to corresponding methods. Controllers are responsible for processing user input, invoking the appropriate business logic, and returning the result to the client.

### Exception:
Exception handling in Spring Boot is typically handled using `@ControllerAdvice` and `@ExceptionHandler` annotations. `@ControllerAdvice` is an annotation that allows you to write global error handling for your application. By annotating a class with `@ControllerAdvice`, you can define methods that handle various exceptions thrown during the execution of controller methods. These methods are annotated with `@ExceptionHandler`, which specifies the type of exception they handle.

### Model:
In Spring Boot, the term "Model" refers to the data that is being transferred between the controller and the view layer of the application. It typically represents the application's business data and encapsulates the state of the application. In Spring MVC, the Model interface or ModelAndView class is used to pass data from the controller to the view. In Spring Boot, this concept is often extended with the use of DTOs (Data Transfer Objects) or entity classes that represent the domain model of the application.

Example:

```java
import lombok.*;

import jakarta.persistence.*;

@Setter
@Getter
@AllArgsConstructor
@NoArgsConstructor
@Builder

@Entity
@Table(name = "employees")
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private long id;

    @Column(name = "first_name", nullable = false)
    private String firstName;

    @Column(name = "last_name", nullable = false)
    private String lastName;

    @Column(nullable = false)
    private String email;
}
```

### Repository:
Repositories in Spring Boot are components responsible for interacting with the database. They are typically interfaces that extend Spring Data's Repository interface or one of its subinterfaces (e.g., CrudRepository, PagingAndSortingRepository). These interfaces provide methods for performing CRUD (Create, Read, Update, Delete) operations on the underlying database entities. Spring Boot's data access framework, along with its JPA (Java Persistence API) or other data access technologies, implements these repository interfaces at runtime, providing boilerplate code for database operations.

Example:

```java

import net.javaguides.springboot.model.Employee;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.query.Param;

import java.util.Optional;

public interface EmployeeRepository extends JpaRepository<Employee, Long> {
    
}
```

### Service:
In Spring Boot, a service is a class annotated with `@Service` that contains business logic and performs operations on data retrieved from repositories. Services encapsulate the application's business logic and are responsible for coordinating the interaction between different components of the application. They abstract away the details of data access and manipulation, allowing controllers to remain focused on handling HTTP requests and responses. Services often collaborate with repositories to retrieve and manipulate data, and they may also perform other tasks such as validation, transformation, and orchestration of multiple operations.

Example:


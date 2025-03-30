# Spring-Boot-Basics
Basics on spring boot applications and how to work with it.

What is Spring Boot?

Spring Boot is an open-source Java-based framework used to create standalone, production-ready Spring applications with minimal configuration. It is built on top of the Spring Framework and simplifies dependency management, configuration, and deployment.

Key Features of Spring Boot:

Auto-Configuration: Automatically configures Spring applications based on the dependencies present in your project.

Standalone: No need for a standalone application server; embedded servers like Tomcat, Jetty, or Undertow are provided.

Dependency Management: Comes with a starter dependency system for quick setup.

Production Ready: Includes features like monitoring, health checks, and metrics

Microservices Support: Widely used for developing microservices architectures.

Steps to Create a Spring Boot Application

1. Set Up the Environment

   Install Java Development Kit (JDK) (version 8 or higher).
   Install a build tool: Maven or Gradle.
   Install an Integrated Development Environment (IDE), e.g., IntelliJ IDEA, Eclipse, or VS Code.

2. Use Spring Initializr

   Visit https://start.spring.io/.
   Fill in the project details (group, artifact, dependencies, etc.).
   Add necessary dependencies (e.g., Spring Web, Spring Data JPA, MySQL Driver).
   Generate the project and download the  file
   Extract the project and open it in your preferred IDE.

3. Create the Main Application Class
The main class should be annotated with @SpringBootApplication.

Example:

package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}

4. Add Dependencies in pom.xml or build.gradle
 
For Maven ():
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>

For Gradle ():
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
}

5. Create REST Controller
Annotate your controller class with @RestController and map endpoints using @getMapping, @PostMapping, etc.

Example:

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, Spring Boot!";
    }
}

6. Run the Application
Run the main method in your DemoApplication class.
The application will start on http://localhost:8080 (default port)  

7. Test the Application
Use a browser, Postman, or curl to test endpoints, e.g., http://localhost:8080/hello.

Common Annotations in Spring Boot

@SpringBootApplication: Combines @configuration, @ComponentScan, and @EnableAutoConfiguration.

@RestController: Indicates the class handles HTTP requests.

@GetMapping, @PostMapping, etc.: Maps HTTP endpoints to methods.

@Entity: Marks a class as a database entity.

@Repository: Indicates a Data Access Object (DAO).

@Service: Denotes the service layer.

@Autowired: Automatically injects dependencies.

Working with Databases
1. Add JPA and Database Dependency: For example, add the following to pom.xml:

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>

2. Configure Application Properties: Add these in application.properties:

spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update

3. Create an Entity Class:

import jakarta.persistence.Entity;
import jakarta.persistence.Id;

@Entity
public class User {
    @Id
    private Long id;
    private String name;
    
    // Getters and Setters
}

4. Create a Repository Interface:

import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
}

5. Use the Repository in Your Service:

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;

    public void saveUser(User user) {
        userRepository.save(user);
    }
}

Spring Boot CLI Commands

Run the application: mvn spring-boot:run or gradle bootRun

Package the application: mvn package or gradle build

Run the JAR file: java -jar target/demo-0.0.1-SNAPSHOT.jar


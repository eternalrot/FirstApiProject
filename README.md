# First REST API – Spring Boot Product Management

## 📌 Project Description

This project is a simple **RESTful API** built with **Spring Boot** that manages products.
It allows users to **create, read, update, delete, and list products**, and demonstrates how to build a layered backend application using **Spring Web, Spring Data JPA, and an H2 in-memory database**.

The project was created as part of an academic assignment and focuses on:
- REST API design
- Exception handling
- Database integration with JPA & Hibernate
- API testing using Postman and Swagger

---

## ⚙️ Features

- Create a new product
- Get a product by ID
- Get all products
- Update an existing product
- Delete a product
- Global exception handling (`@ControllerAdvice`)
- In-memory H2 database with web console
- Clean layered architecture (Controller → Service → Repository)

---

## 🧰 Tech Stack

**Backend**
- Java 17+
- Spring Boot
- Spring Web (REST API)
- Spring Data JPA
- Hibernate

**Database**
- H2 (in-memory database)

**Tools**
- Maven
- Postman (API testing)
- Swagger / OpenAPI (API documentation)
- IntelliJ IDEA

---

## 📁 Project Structure

- `src/main/java/pl/edu/vistula/firstrestapispring/FirstRestApiSpringApplication.java`  
  — main Spring Boot application entry point

- `src/main/java/pl/edu/vistula/firstrestapispring/product/api/ProductController.java`  
  — REST controller with CRUD endpoints for products

- `src/main/java/pl/edu/vistula/firstrestapispring/product/api/request/`  
  — request DTOs (`ProductRequest`, `UpdateProductRequest`)

- `src/main/java/pl/edu/vistula/firstrestapispring/product/api/response/`  
  — response DTOs (`ProductResponse`)

- `src/main/java/pl/edu/vistula/firstrestapispring/product/domain/Product.java`  
  — JPA entity representing a product

- `src/main/java/pl/edu/vistula/firstrestapispring/product/repository/ProductRepository.java`  
  — Spring Data JPA repository

- `src/main/java/pl/edu/vistula/firstrestapispring/product/service/ProductService.java`  
  — business logic layer

- `src/main/java/pl/edu/vistula/firstrestapispring/product/support/ProductMapper.java`  
  — maps DTOs to entities and responses

- `src/main/java/pl/edu/vistula/firstrestapispring/product/support/ProductExceptionAdvisor.java`  
  — global exception handler (`@ControllerAdvice`)

- `src/main/java/pl/edu/vistula/firstrestapispring/shared/api/response/ErrorMessageResponse.java`  
  — common error response model

- `src/main/resources/application.properties`  
  — application configuration (H2, logging, app name)

---

## 🔁 Application Flow

1. **Controller** receives HTTP requests
2. **Service** contains business logic
3. **Repository** communicates with the database
4. **Mapper** converts entities to DTOs and vice versa
5. **Exception Advisor** handles errors globally and returns proper HTTP responses

---

## 🧠 How ProductRepository Works

Although `ProductRepository` does not explicitly implement methods like `save`, `findById`, or `deleteById`, it extends `JpaRepository`.
Spring Data JPA automatically provides implementations for these methods at runtime using dynamic proxy generation.

This allows developers to focus on business logic instead of writing boilerplate database code.

---

## 🧪 Testing

- All endpoints were tested using Postman
- Database state was verified using H2 Console
- Exception handling was tested by requesting non-existing resources

---

## 🌐 API Endpoints Overview

This project exposes a simple REST API for managing Product resources.
The API supports full CRUD operations and follows standard REST conventions.

1. Using the **POST** method, a new product can be created by sending its data in JSON format to the /api/v1/products endpoint.
   - http://localhost:8080/api/v1/products
     
     ![image alt](https://github.com/eternalrot/FirstApiProject/blob/main/imagePOST.png?raw=true)
     
2. The **GET** method allows retrieving a single product by its identifier (/api/v1/products/{id}) or fetching all existing products (/api/v1/products).
   - http://localhost:8080/api/v1/products/1
     
     ![image alt](https://github.com/eternalrot/FirstApiProject/blob/main/imageGET.png?raw=true)
     
3. Product data can be updated using the **PUT** method with the product ID specified in the URL and the new values provided in the request body.
   - http://localhost:8080/api/v1/products/1
     
     ![image alt](https://github.com/eternalrot/FirstApiProject/blob/main/imagePUT.png?raw=true)
     
4. Finally, the **DELETE** method enables removing a product from the system by its ID.
   - http://localhost:8080/api/v1/products/1
     
     ![image alt](https://github.com/eternalrot/FirstApiProject/blob/main/imageDELETE.png?raw=true)
     
All endpoints return JSON responses and appropriate HTTP status codes, making the API easy to test using tools such as Postman or Swagger.

---

## 🗄️ Database (H2)

This project uses an H2 in-memory database, which exists only while the application is running.

1. Enable H2 Console

**application.properties:**

```properties
  spring.application.name=First-Rest-Api-Spring
  spring.h2.console.enabled=true
  spring.h2.console.path=/console/
  spring.datasource.url=jdbc:h2:mem:testdb;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE
  logging.level.org.hibernate.SQL=DEBUG
```

2. Open H2 Console
  - http://localhost:8080/console
  - JDBC URL: jdbc:h2:mem:testdb
  - User: sa
  - Password: (empty)

3. View All Products in Database
  - SELECT * FROM PRODUCTS;

    ![image alt](https://github.com/eternalrot/FirstApiProject/blob/main/imageDATABASE.png?raw=true)

---

## 📖 What This Project Demonstrates

- Proper REST API design
- Separation of concerns
- DTO usage (Request / Response objects)
- Global exception handling
- JPA repository abstraction
- In-memory database usage for development

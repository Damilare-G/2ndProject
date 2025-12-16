# Spring Framework Application – Task 2 (REST API)

This repository contains a **Spring Boot REST API application** developed as **Task 2** for the *Spring Framework Apps – Projects for Everyone* assignment at **Akademia Finansów i Biznesu Vistula**.

The project demonstrates a complete backend application built with Spring Boot, including layered architecture, REST endpoints, exception handling, Swagger documentation, and database integration.

---

## 🔹 Task 2 – REST API with Spring Boot

### 📌 Objective

Task 2 focuses on building a **RESTful backend application** that:

* Exposes REST endpoints using HTTP methods
* Applies layered architecture (Controller, Service, Repository)
* Uses DTOs and object mapping
* Implements exception handling
* Documents the API with Swagger (OpenAPI)
* Persists data using an H2 database and Spring Data JPA

---

### 🛠️ Technologies Used

* Java
* Spring Boot
* Spring Web
* Spring Data JPA
* H2 Database
* Swagger / OpenAPI
* Maven
* Postman / Swagger UI

---

### 🔄 Application Flow Overview

1. Client sends an HTTP request (JSON)
2. Controller receives request and maps it to a DTO
3. Service layer applies business logic
4. Repository persists or retrieves data
5. Mapper converts entities ↔ DTOs
6. Controller returns HTTP response with proper status

---

### 📡 REST Endpoints

| Method | Endpoint                | Description       | Status         |
| ------ | ----------------------- | ----------------- | -------------- |
| POST   | `/api/v1/products`      | Create a product  | 201 Created    |
| GET    | `/api/v1/products/{id}` | Get product by ID | 200 OK         |
| GET    | `/api/v1/products`      | Get all products  | 200 OK         |
| PUT    | `/api/v1/products/{id}` | Update product    | 200 OK         |
| DELETE | `/api/v1/products/{id}` | Delete product    | 204 No Content |

---

### 🧾 Example JSON Requests

**Create Product (POST)**

```json
{
  "name": "Laptop"
}
```

**Update Product (PUT)**

```json
{
  "name": "MacBook"
}
```

---

### ❗ Exception Handling

* Custom exception: `ProductNotFoundException`
* Centralized handling using `@ControllerAdvice`
* Proper HTTP status codes returned (e.g. 404 NOT FOUND)
* Error response wrapped in `ErrorMessageResponse`

---

### 📘 Swagger, POSTMAN / OpenAPI

Swagger UI is enabled for API documentation and testing.

* **Swagger UI**:

  ```
  http://localhost:8080/swagger-ui/index.html
  ```
* **OpenAPI JSON**:

  ```
  http://localhost:8080/v1/api-docs
  ```
* **POSTMAN**:

  ```
  http://localhost:8080/api/v1/products
  ```

---

### 🗄️ Database Integration (H2 + JPA)

* In-memory H2 database
* Hibernate automatically generates tables
* Entity mapping using `@Entity`, `@Id`, `@GeneratedValue`
* Repository extends `JpaRepository<Product, Long>`

**H2 Console**:

```
http://localhost:8080/console
JDBC URL: jdbc:h2:mem:testdb
```

---

### 🧪 Testing

* Endpoints tested using:

    * Swagger UI
    * Postman
    * Browser (GET requests)
* Full CRUD operations verified
* Exception cases tested (non-existing IDs)

---

### ✅ Learning Outcomes (Task 2)

* Building REST APIs with Spring Boot
* Applying clean architecture and best practices
* Using DTOs and object mapping
* Handling exceptions correctly
* Documenting APIs with Swagger
* Using Spring Data JPA and H2 database

---

## ❓ Lecturer’s Question (Slide 63)

### Why does `JpaRepository` work without method implementations?

In the final stage of Task 2, the `ProductRepository` is defined as:

```java
public interface ProductRepository extends JpaRepository<Product, Long> {
}
```

Even though this interface **does not contain any method implementations**, the application still works and methods such as:

* `save()`
* `findById()`
* `findAll()`
* `deleteById()`

are available and fully functional.

#### Explanation

This works because:

1. **Spring Data JPA provides the implementation automatically at runtime**.

    * `JpaRepository` is part of Spring Data JPA.
    * Spring uses **dynamic proxy generation** and **reflection** to create a concrete class behind the scenes.

2. **Method implementations are generated based on interfaces**.

    * When the application starts, Spring scans repository interfaces.
    * It detects `JpaRepository<Product, Long>` and generates an implementation that knows how to:

        * persist entities
        * execute SQL queries
        * map database rows to Java objects

3. **Hibernate handles the actual database operations**.

    * Hibernate is the JPA provider.
    * It translates method calls (e.g. `save`) into SQL queries.

4. **This follows the Inversion of Control (IoC) principle**.

    * Developers only define *what* they need (the interface).
    * Spring decides *how* it is implemented.

Because of this mechanism, **no manual implementation is required**, and the repository remains clean, readable, and easy to maintain.

This approach is one of the key advantages of using **Spring Data JPA**.

---

## 📌 Final Notes

* Code is version-controlled using Git
* `.gitignore` is included to exclude unnecessary files
* Applications are ready for live demonstration and testing

---

Screenshots of All Methods Used.
![2A First postman.png](src/main/resources/static/images/2A%20First%20postman.png)
![2B Swagger JSON.png](src/main/resources/static/images/2B%20Swagger%20JSON.png)
![2B Swagger UI second.png](src/main/resources/static/images/2B%20Swagger%20UI%20second.png)
![2B Swagger UI.png](src/main/resources/static/images/2B%20Swagger%20UI.png)
![2C Another Endpoint in normal browser.png](src/main/resources/static/images/2C%20Another%20Endpoint%20in%20normal%20browser.png)
![2C Another Endpoint in Postman.png](src/main/resources/static/images/2C%20Another%20Endpoint%20in%20Postman.png)
![2C Another Endpoint in Swagger.png](src/main/resources/static/images/2C%20Another%20Endpoint%20in%20Swagger.png)
![2E Postman Exception handling.png](src/main/resources/static/images/2E%20Postman%20Exception%20handling.png)
![2E Postman GET after PUT.png](src/main/resources/static/images/2E%20Postman%20GET%20after%20PUT.png)
![2E Postman POST to create new product.png](src/main/resources/static/images/2E%20Postman%20POST%20to%20create%20new%20product.png)
![2E Postman PUT.png](src/main/resources/static/images/2E%20Postman%20PUT.png)
![2E Postman to get new product created after POST.png](src/main/resources/static/images/2E%20Postman%20to%20get%20new%20product%20created%20after%20POST.png)
![2E Swagger Exception Handling.png](src/main/resources/static/images/2E%20Swagger%20Exception%20Handling.png)
![2E Swagger GET after PUT.png](src/main/resources/static/images/2E%20Swagger%20GET%20after%20PUT.png)
![2E Swagger GET response after new product created.png](src/main/resources/static/images/2E%20Swagger%20GET%20response%20after%20new%20product%20created.png)
![2E Swagger POST to create new product.png](src/main/resources/static/images/2E%20Swagger%20POST%20to%20create%20new%20product.png)
![2E Swagger PUT.png](src/main/resources/static/images/2E%20Swagger%20PUT.png)
![2F Creating Product .png](src/main/resources/static/images/2F%20Creating%20Product%20.png)
![2F Deleting existing product.png](src/main/resources/static/images/2F%20Deleting%20existing%20product.png)
![2F Deleting non existing product.png](src/main/resources/static/images/2F%20Deleting%20non%20existing%20product.png)
![2G Adding Database i.png](src/main/resources/static/images/2G%20Adding%20Database%20i.png)
![2G Adding Database ii.png](src/main/resources/static/images/2G%20Adding%20Database%20ii.png)
![2G Adding Database iii BIGINT.png](src/main/resources/static/images/2G%20Adding%20Database%20iii%20BIGINT.png)
![2H Testing i POST Console.png](src/main/resources/static/images/2H%20Testing%20i%20POST%20Console.png)
![2H Testing i POST.png](src/main/resources/static/images/2H%20Testing%20i%20POST.png)
![2H Testing ii GET.png](src/main/resources/static/images/2H%20Testing%20ii%20GET.png)
![2H Testing iii PUT CONSOLE.png](src/main/resources/static/images/2H%20Testing%20iii%20PUT%20CONSOLE.png)
![2H Testing iii PUT.png](src/main/resources/static/images/2H%20Testing%20iii%20PUT.png)
![2H Testing iv GET all products.png](src/main/resources/static/images/2H%20Testing%20iv%20GET%20all%20products.png)
![2H Testing v DELETE COSOLE.png](src/main/resources/static/images/2H%20Testing%20v%20DELETE%20COSOLE.png)
![2H Testing v DELETE.png](src/main/resources/static/images/2H%20Testing%20v%20DELETE.png)
![2H Testing vi GET error test for non existing product.png](src/main/resources/static/images/2H%20Testing%20vi%20GET%20error%20test%20for%20non%20existing%20product.png)
![2H Testing vii DELETE error test for non existing product CONSOLE.png](src/main/resources/static/images/2H%20Testing%20vii%20DELETE%20error%20test%20for%20non%20existing%20product%20CONSOLE.png)
![2H Testing vii DELETE error test for non existing product.png](src/main/resources/static/images/2H%20Testing%20vii%20DELETE%20error%20test%20for%20non%20existing%20product.png)
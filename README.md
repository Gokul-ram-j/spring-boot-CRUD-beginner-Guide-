# Spring Boot CRUD API - Beginner Guide

A simple Spring Boot application demonstrating basic CRUD (Create, Read, Update, Delete) operations with MySQL database using JPA/Hibernate.

## 📋 Table of Contents
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Prerequisites](#prerequisites)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [API Endpoints](#api-endpoints)
- [Database Configuration](#database-configuration)
- [Usage Examples](#usage-examples)
- [Learning Resources](#learning-resources)

## ✨ Features

- **CRUD Operations**: Create, Read, Update, and Delete users
- **RESTful API**: Clean REST endpoints following best practices
- **Database Integration**: MySQL database with JPA/Hibernate
- **Custom Queries**: Native SQL queries for complex filtering
- **Multiple Data Retrieval Methods**: Path variables, request parameters, and request body
- **Response Entity Handling**: Proper HTTP status codes and responses

## 🛠 Technologies Used

- **Spring Boot** - Main framework
- **Spring Data JPA** - Data access layer
- **MySQL** - Database
- **Maven** - Dependency management
- **Java** - Programming language

## 📋 Prerequisites

Before running this application, make sure you have:

- Java 17 or higher
- Maven 3.6+
- MySQL 8.0+
- IDE (IntelliJ IDEA, Eclipse, or VS Code)

## 🚀 Getting Started

### 1. Clone the Repository
```bash
git clone <repository-url>
cd spring-boot-crud-guide
```

### 2. Database Setup
1. Install and start MySQL server
2. Create a new database:
```sql
CREATE DATABASE springboot;
```

### 3. Configure Database Connection
Update `src/main/resources/application.properties` with your MySQL credentials:
```properties
spring.application.name=JPAdemo

spring.jpa.hibernate.ddl-auto=update
spring.datasource.url=jdbc:mysql://localhost:3306/springboot
spring.datasource.username=your_username
spring.datasource.password=your_password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.show-sql=true
```

### 4. Run the Application
```bash
mvn spring-boot:run
```

The application will start on `http://localhost:8080`

## 📁 Project Structure

```
src/main/java/com/example/JPAdemo/
├── controller/
│   └── UserController.java    # REST API endpoints
├── model/
│   └── UserModel.java         # Entity class
├── repository/
│   └── UserRepo.java          # Data access layer
└── service/
    └── UserService.java       # Business logic layer
```

### Architecture Overview

- **Controller Layer**: Handles HTTP requests and responses
- **Service Layer**: Contains business logic
- **Repository Layer**: Data access and database operations
- **Model Layer**: Entity classes representing database tables

## 🔗 API Endpoints

| Method | Endpoint | Description | Request Body |
|--------|----------|-------------|--------------|
| `GET` | `/user` | Get all users | None |
| `POST` | `/user` | Create a new user | UserModel JSON |
| `PUT` | `/user` | Update existing user | UserModel JSON |
| `DELETE` | `/user/{id}` | Delete user by ID | None |
| `GET` | `/user/dept/{dept}` | Get users by department | None |
| `GET` | `/user/filter/aboveAge?age={age}` | Get users above age | None |
| `GET` | `/user/filter/belowAge?age={age}` | Get users below age | None |
| `GET` | `/filter?name={name}&age={age}` | Filter demo endpoint | None |

## 🗄 Database Configuration

The application uses MySQL with the following table structure:

```sql
CREATE TABLE user_model (
    id INT PRIMARY KEY,
    name VARCHAR(255),
    dept VARCHAR(255),
    age INT
);
```

**Note**: The table is automatically created by Hibernate due to `spring.jpa.hibernate.ddl-auto=update`

## 📝 Usage Examples

### Create a User
```bash
curl -X POST http://localhost:8080/user \
  -H "Content-Type: application/json" \
  -d '{
    "id": 1,
    "name": "John Doe",
    "dept": "Engineering",
    "age": 25
  }'
```

### Get All Users
```bash
curl -X GET http://localhost:8080/user
```

### Get Users by Department
```bash
curl -X GET http://localhost:8080/user/dept/Engineering
```

### Update a User
```bash
curl -X PUT http://localhost:8080/user \
  -H "Content-Type: application/json" \
  -d '{
    "id": 1,
    "name": "John Smith",
    "dept": "Engineering",
    "age": 26
  }'
```

### Delete a User
```bash
curl -X DELETE http://localhost:8080/user/1
```

### Filter Users Above Age
```bash
curl -X GET http://localhost:8080/user/filter/aboveAge?age=20
```

## 🎓 Learning Resources

This project demonstrates several important Spring Boot concepts:

### Key Annotations Explained

- `@RestController`: Combines `@Controller` and `@ResponseBody`
- `@Autowired`: Enables dependency injection
- `@Entity`: Marks a class as a JPA entity
- `@Id`: Specifies the primary key
- `@Service`: Marks a class as a service component
- `@Repository`: Marks an interface as a repository

### HTTP Methods Used

- **GET**: Retrieve data
- **POST**: Create new resources
- **PUT**: Update existing resources
- **DELETE**: Remove resources

### Data Handling Methods

1. **@RequestBody**: Get data from request body
2. **@PathVariable**: Get data from URL path
3. **@RequestParam**: Get data from query parameters

### Repository Pattern

The `UserRepo` interface extends `JpaRepository` which provides:
- Basic CRUD operations
- Custom query methods (`findBy*`)
- Native SQL queries with `@Query`

## 🤝 Contributing

This is a beginner-friendly project! Feel free to:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🐛 Common Issues

**Issue**: Application fails to start with database connection error
**Solution**: Ensure MySQL is running and credentials in `application.properties` are correct

**Issue**: Table not found error
**Solution**: Make sure `spring.jpa.hibernate.ddl-auto=update` is set in properties file

**Issue**: 404 Not Found for API endpoints
**Solution**: Verify the application is running on the correct port (8080 by default)

---

Happy Coding! 🚀

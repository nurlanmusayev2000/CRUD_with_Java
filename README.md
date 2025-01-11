# Simple CRUD API with Authentication

## Overview
This is a Spring Boot application implementing a simple CRUD API with authentication. The application supports user registration, login, viewing all users, updating user details, and deleting users. Authentication is managed using JWT (JSON Web Tokens). The application uses a PostgreSQL database running inside a Docker container.

---

## Features
- **Register a user**: `/register`
- **Login and receive a JWT token**: `/login`
- **View all users (authenticated)**: `/users`
- **Update user details (authenticated)**: `/users/{id}`
- **Delete a user by ID (authenticated)**: `/users/{id}`

---

## Requirements
- **Java**: Version 17 or higher
- **Maven**: Version 3.6 or higher
- **Docker**: Version 20.10 or higher
- **Postman**: (Optional) for testing the API

---

## Getting Started

### Step 1: Clone the Repository
```bash
git clone <repository_url>
cd <repository_name>
```

### Step 2: Run PostgreSQL in Docker
1. Ensure Docker Desktop is running.
2. Start PostgreSQL:
   ```bash
   docker run --name postgres-container -e POSTGRES_USER=admin -e POSTGRES_PASSWORD=admin -e POSTGRES_DB=mydb -p 5432:5432 -d postgres:latest
   ```
3. Verify the container is running:
   ```bash
   docker ps
   ```

---

### Step 3: Configure Application Properties
Edit the `src/main/resources/application.properties` file to match your database setup:
```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/mydb
spring.datasource.username=admin
spring.datasource.password=admin
spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect

# JWT Secret Key
jwt.secret=YourSuperSecretKeyThatIsAtLeast32CharactersLong
```

---

### Step 4: Build and Run the Application
1. Build the project:
   ```bash
   mvn clean install
   ```
2. Start the application:
   ```bash
   mvn spring-boot:run
   ```

---

## API Endpoints

### 1. **Register User**
- **Endpoint**: `POST /register`
- **Request Body**:
  ```json
  {
      "username": "testuser",
      "password": "password123"
  }
  ```
- **Response**:
  ```json
  {
      "message": "User registered successfully"
  }
  ```

---

### 2. **Login**
- **Endpoint**: `POST /login`
- **Request Body**:
  ```json
  {
      "username": "testuser",
      "password": "password123"
  }
  ```
- **Response**:
  ```json
  {
      "token": "your-jwt-token"
  }
  ```

---

### 3. **Get All Users**
- **Endpoint**: `GET /users`
- **Headers**:
  ```
  Authorization: Bearer <your-jwt-token>
  ```
- **Response**:
  ```json
  [
      {
          "id": 1,
          "username": "testuser",
          "password": "encrypted-password"
      }
  ]
  ```

---

### 4. **Update User**
- **Endpoint**: `PUT /users/{id}`
- **Headers**:
  ```
  Authorization: Bearer <your-jwt-token>
  ```
- **Request Body**:
  ```json
  {
      "username": "newUsername",
      "password": "newPassword"
  }
  ```
- **Response**:
  ```json
  {
      "message": "User updated successfully"
  }
  ```

---

### 5. **Delete User**
- **Endpoint**: `DELETE /users/{id}`
- **Headers**:
  ```
  Authorization: Bearer <your-jwt-token>
  ```
- **Response**:
  ```json
  {
      "message": "User deleted successfully"
  }
  ```

---

## Testing with Postman
1. Open Postman and create a new collection.
2. Add requests for each endpoint (`/register`, `/login`, `/users`, `/users/{id}`).
3. Set the `Authorization` header with the JWT token for authenticated endpoints.
4. Test each endpoint to verify functionality.

---

## Future Improvements
- Add unit and integration tests using JUnit and Mockito.
- Implement role-based access control.
- Add more detailed error handling and validation.
- Dockerize the entire application for easier deployment.



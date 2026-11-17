# Spring Boot JWT Authentication Demo

A beginner-friendly Spring Boot JWT example using Java 21, Spring Security, Spring Data JPA, H2, and JJWT.

## Requirements
- JDK 21
- Maven 3.6+ (or use the Maven wrapper if you add one)
- IntelliJ IDEA, STS, or VS Code

## Run
From this folder:

```bash
mvn spring-boot:run
```

Application URL: `http://localhost:8080`

## Test with Postman

### 1. Register
- Method: `POST`
- URL: `http://localhost:8080/api/auth/register`
- Header: `Content-Type: application/json`
- Body (raw JSON):

```json
{
  "username": "akshaya",
  "password": "password123"
}
```

Expected: HTTP `201 Created`.

### 2. Login and get JWT
- Method: `POST`
- URL: `http://localhost:8080/api/auth/login`
- Header: `Content-Type: application/json`
- Body:

```json
{
  "username": "akshaya",
  "password": "password123"
}
```

Copy the `token` value from the response.

### 3. Call protected endpoint
- Method: `GET`
- URL: `http://localhost:8080/api/demo/hello`
- Authorization tab: choose `Bearer Token` and paste the token.

Expected response:

```json
{
  "message": "You accessed a protected endpoint successfully",
  "username": "akshaya"
}
```

Without a valid token, the protected endpoint returns `401 Unauthorized`.

## JWT parts
The token has three Base64URL-encoded parts separated by dots:

`header.payload.signature`

- Header: token type and signing algorithm.
- Payload: claims such as username and expiry.
- Signature: verifies token integrity and authenticity.

The `jwt.secret` in `application.properties` is a demonstration-only Base64 secret for HMAC signing. Do not use this demo key in production. Keep real secrets outside source control, use a strong randomly generated key, and rotate it if exposed.

## Notes
- H2 is an in-memory database. Users are removed when the application stops.
- Passwords are stored as BCrypt hashes.
- This is a learning example, not a complete production identity system.

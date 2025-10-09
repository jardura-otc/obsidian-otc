# CLAUDE.md

  

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

  

## Project Overview

  

**Wattson Backend** is a Spring Boot 3.2.5 application for managing electric vehicle charging infrastructure. It provides REST APIs for managing chargers, batteries, vehicles (vans), charging sessions, assignments, and user authentication.

  

## Technology Stack

  

- **Framework**: Spring Boot 3.2.5 with Java 17

- **Database**: PostgreSQL with MyBatis for data access

- **Security**: Spring Security with JWT authentication

- **API Documentation**: OpenAPI 3 (Swagger)

- **Build Tool**: Maven

- **Testing**: JUnit 5, Mockito, Spring Boot Test

  

## Architecture

  

### Layered Architecture Pattern

  

The application follows a standard three-layer architecture:

  

1. **Controller Layer** (`controller/`): REST endpoints with Swagger annotations

2. **Service Layer** (`service/`): Business logic and transactional operations

3. **Mapper Layer** (`mapper/`): MyBatis interfaces with SQL annotations for database operations

  

### Core Components

  

- **Authentication Flow**: JWT-based authentication with refresh tokens

  - `AuthUserController`: Handles login, logout, and token refresh

  - `JwtAuthFilter`: Validates JWT tokens on protected endpoints

  - `JwtUtil`: Token generation and validation utilities

  - `RefreshTokenService`: Manages refresh token lifecycle

  - `UserDetailsServiceImp`: Loads user details for Spring Security

  

- **Security Configuration** (`configSecurity/`):

  - JWT filter chain configured in `SecurityConfig`

  - Public endpoints: `/auth/login`, `/auth/refresh-token`, Swagger UI

  - All other endpoints require authentication

  - `SecurityExceptionHandler`: Custom authentication/authorization error handling

  

- **Exception Handling**:

  - `GlobalExceptionHandler`: Handles validation, business logic, and HTTP errors

  - `SecurityExceptionHandler`: Handles authentication and authorization failures

  - `ApiError`: Standardized error response format

  

### Data Model

  

Key entities managed by the system:

- **Users**: Authentication and role-based access control

- **Chargers**: Physical charging devices at locations

- **Batteries**: Battery units being charged/managed

- **Vans**: Vehicles in the system

- **Sessions**: Charging session tracking with status management

- **Assignments**: Linking resources together

- **Hubs/Clients**: Organizational entities

- **Models**: Van models and battery models

  

### MyBatis Configuration

  

- Mappers use annotation-based SQL (no XML files)

- Automatic camel case to underscore conversion enabled

- Mapper interfaces in `mapper/` package are auto-scanned via `@MapperScan`

  

### Environment Profiles

  

Multiple Spring profiles for different environments:

- `local`: Local development (port 8080, local PostgreSQL)

- `localDocker`: Docker-based local development

- `dev`: Development environment

- `pre`: Pre-production environment

- `prd`: Production environment

  

Profile-specific properties in `application-{profile}.properties`

  

## Common Commands

  

### Build and Run

  

```bash

# Build the project

mvn clean package

  

# Run the application (local profile by default)

mvn spring-boot:run

  

# Run with specific profile

mvn spring-boot:run -Dspring-boot.run.arguments=--spring.profiles.active=local

  

# Build without tests

mvn clean package -DskipTests

```

  

### Testing

  

```bash

# Run all tests

mvn test

  

# Run a specific test class

mvn test -Dtest=UserServiceTest

  

# Run a specific test method

mvn test -Dtest=UserServiceTest#testMethodName

  

# Run tests with coverage

mvn clean test jacoco:report

```

  

### Database

  

The application uses PostgreSQL with schema `data`. Schema initialization SQL is in `src/main/resources/sql/schema.sql`.

  

Default credentials for local development:

- Database: `wattson` (schema: `data`)

- Username: `postgres`

- Password: `1234`

  

Default users created in schema:

- Admin: `admin@admin.com` / password: `password` (bcrypt encoded)

- User: `user@user.com` / password: `password` (bcrypt encoded)

  

### API Documentation

  

Once running, access Swagger UI at:

```

http://localhost:8080/swagger-ui/index.html

```

  

### Required Request Headers

  

Most authenticated endpoints require:

- `Authorization: Bearer <jwt_token>`

- `Content-Type: application/json`

  

Some endpoints may also use:

- `X-Tenant-ID`: For multi-tenancy support

  

### Docker

  

```bash

# Build Docker image

./infrastructure/scripts/container-build.sh

  

# Build and push to AWS ECR

./infrastructure/scripts/container-build-and-push.sh <ENV> <VERSION> -y

```

  

## Development Workflow

  

### Creating New Entities

  

1. Create entity class in `entity/` with Lombok annotations

2. Create mapper interface in `mapper/` with MyBatis annotations

3. Create service class in `service/` with `@Service` and `@Transactional`

4. Create controller in `controller/` with `@RestController` and Swagger annotations

5. Add DTOs in `dto/request/` and `dto/response/` if needed

  

### Authentication Implementation

  

- User passwords are encoded with BCrypt via `DelegatingPasswordEncoder`

- JWT tokens expire based on `application.security.jwt-ttl` (milliseconds)

- Refresh tokens have 30-day expiration by default

- On refresh, old refresh tokens are revoked and new ones issued

  

### Security Best Practices

  

- Never commit secrets or credentials to version control

- Use environment-specific properties files

- All database operations in services should be `@Transactional`

- Use `PasswordEncoder.encode()` for all password storage

- JWT secret keys must be at least 256 bits (32 characters)

  

### Error Handling Pattern

  

Service layer throws domain exceptions:

- `IllegalArgumentException` for business rule violations (returns 400)

- `NoSuchElementException` for not found scenarios (returns 404)

- `UsernameNotFoundException` for authentication failures

  

Controllers catch and transform via `GlobalExceptionHandler`.

  

## CI/CD

  

GitHub Actions workflow (`.github/workflows/build-and-push-ecr.yml`):

- Manual trigger via workflow_dispatch

- Builds Docker image and pushes to AWS ECR

- Supports DEV, PRE, and PROD environments

- Requires AWS credentials in GitHub Secrets

  

## Main Branch Strategy

  

- Main development branch: `develop`

- Feature branches should be created from `develop`

- Pull requests should target `develop`
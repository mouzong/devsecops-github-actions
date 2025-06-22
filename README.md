# Goldencat BankApp

A secure, full-stack banking web application built with Spring Boot, MySQL, and Thymeleaf. This project demonstrates modern DevSecOps practices, including CI/CD, security scanning, containerization, and Kubernetes deployment.

## Features

- User registration and authentication (Spring Security)
- Account dashboard with balance and transaction history
- Deposit, withdraw, and transfer money between users
- Responsive UI with Bootstrap and Thymeleaf
- MySQL database integration
- Secure password storage (BCrypt)
- Role-based access control
- CI/CD pipeline with GitHub Actions
- Security scanning (Trivy, Gitleaks, SonarQube)
- Dockerized build and deployment
- Kubernetes manifests for deployment

## Project Structure

```
src/
  main/
    java/com/example/bankapp/      # Java source code (controllers, services, models, repositories)
    resources/
      templates/                   # Thymeleaf HTML templates
      static/                      # Static resources
      application.properties       # Spring Boot configuration
  test/
    java/com/example/bankapp/      # Unit tests
.github/
  workflows/                       # GitHub Actions CI/CD pipeline
Dockerfile                         # Docker build file
ds.yml                             # Kubernetes manifests
pom.xml                            # Maven build file
```

## Getting Started

### Prerequisites

- Java 17+
- Maven 3.9+
- MySQL 8+
- Docker (for containerization)
- Kubernetes (for deployment)

### Local Development

1. **Clone the repository:**

   ```sh
   git clone https://github.com/mouzong/devsecops-github-actions.git
   cd bankapp
   ```

2. **Set up the database:**

   - Create a MySQL database named `bankappdb` (see [`src/main/resources/static/mysql/SQLScript.txt`](src/main/resources/static/mysql/SQLScript.txt)).
   - Update credentials in [`src/main/resources/application.properties`](src/main/resources/application.properties) if needed.

3. **Build and run the application:**

   ```sh
   ./mvnw spring-boot:run
   ```

   The app will be available at `http://localhost:8080`.

4. **Access the app:**
   - Register a new user at `/register`
   - Login at `/login`
   - Use the dashboard to deposit, withdraw, transfer, and view transactions

### Running Tests

```sh
./mvnw test
```

### Building Docker Image

```sh
./mvnw package
docker build -t fryker/bankapp:latest .
```

### Running with Docker

```sh
docker run -p 8080:8080 --env SPRING_DATASOURCE_URL=jdbc:mysql://<mysql_host>:3306/bankappdb?useSSL=false --env SPRING_DATASOURCE_USERNAME=root --env SPRING_DATASOURCE_PASSWORD=Test@123 bankapp:latest
```

### Kubernetes Deployment

1. Deploy MySQL and the application using the manifests in [`ds.yml`](ds.yml):

   ```sh
   kubectl apply -f ds.yml
   ```

2. Access the application via the `bankapp-service` LoadBalancer.

## CI/CD & Security

- **CI/CD:** Automated via GitHub Actions ([`.github/workflows/ci.yml`](.github/workflows/ci.yml))
- **Security Scans:** Trivy (vulnerabilities), Gitleaks (secrets), SonarQube (code quality)
- **Docker:** Multi-stage build, image pushed to Docker Hub
- **Kubernetes:** Deployments and services for both MySQL and the app

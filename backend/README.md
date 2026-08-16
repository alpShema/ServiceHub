# ServiceHub

A Spring Boot backend for a service request management system that allows employees to submit and track service requests across departments, with SLA enforcement, role-based access control, and an admin dashboard.

---

## Features

- **Service Request Management** — Create, view, update, and track service requests with priority levels and status transitions
- **Department Routing** — Requests are routed to the appropriate department based on category
- **SLA Enforcement** — Configurable SLA policies per department; automatic deadline tracking
- **Role-Based Access Control** — Three roles: `USER`, `AGENT`, and `ADMIN`, each with scoped permissions
- **Authentication** — JWT-based login and registration with Spring Security
- **Admin Dashboard** — Overview of requests, departments, SLA compliance, and user management
- **Email Notifications** — Automated emails on request creation and status updates
- **API Documentation** — Swagger UI via SpringDoc OpenAPI
- **Observability** — Actuator health/info endpoints with Prometheus metrics

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Java 17 |
| Framework | Spring Boot 3.2 |
| Security | Spring Security + JWT (jjwt 0.12) |
| Database | PostgreSQL (production), H2 (testing) |
| Migrations | Flyway |
| ORM | Spring Data JPA / Hibernate |
| Validation | Spring Validation |
| Templating | Thymeleaf |
| Documentation | SpringDoc OpenAPI (Swagger UI) |
| Metrics | Micrometer + Prometheus |
| Build | Maven |
| Containerization | Docker |

---

## Getting Started

### Prerequisites

- Java 17+
- Maven 3.8+
- PostgreSQL 14+
- Docker (optional)

### Environment Variables

Create an `application.properties` or set these environment variables:

```env
DB_URL=jdbc:postgresql://localhost:5432/servicehub
DB_USERNAME=your_db_user
DB_PASSWORD=your_db_password
JWT_SECRET=your_jwt_secret
MAIL_HOST=smtp.example.com
MAIL_PORT=587
MAIL_USERNAME=your_email
MAIL_PASSWORD=your_email_password
```

### Run Locally

```bash
# Clone the repository
git clone https://github.com/alpShema/ServiceHub.git
cd ServiceHub

# Build
mvn clean install

# Run
mvn spring-boot:run
```

### Run with Docker

```bash
docker build -t servicehub .
docker run -p 8080:8080 --env-file .env servicehub
```

---

## API Documentation

Once the app is running, visit:

```
http://localhost:8080/swagger-ui.html
```

---

## Project Structure

```
src/main/java/com/servicehub/
├── config/          # Security, JWT, and app configuration
├── controller/      # REST and MVC controllers
├── dto/             # Request and response data transfer objects
├── exception/       # Global exception handling
├── init/            # Data initializers (seed roles, admin user)
├── model/           # JPA entities (User, ServiceRequest, Department, SlaPolicy)
│   └── enums/       # Role, RequestStatus, Priority, RequestCategory
├── repository/      # Spring Data JPA repositories
└── service/         # Business logic layer
```

---

## Roles

| Role | Access |
|---|---|
| `USER` | Submit and track own service requests |
| `AGENT` | Handle assigned requests, update status |
| `ADMIN` | Full access — manage users, departments, SLA policies, dashboard |

---

## Health & Metrics

```
GET /actuator/health
GET /actuator/info
GET /actuator/prometheus
```

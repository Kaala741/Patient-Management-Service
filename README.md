# 🏥 Patient Management System — Microservices Architecture

## 📘 About  
A **production-ready, enterprise-grade Patient Management System** built using a fully distributed **microservices architecture**.  
The system is designed with **Spring Boot**, **Kafka**, **gRPC**, **Spring Cloud Gateway**, **Docker**, and **AWS-like deployment via LocalStack**.

This project mimics how real companies build scalable backend platforms—with **event-driven communication**, **API gateways**, **service-level isolation**, **dedicated databases**, and **secure authentication (JWT)**.

---

# 🚀 Key Features

- 🧩 **Microservices Architecture** — Each domain is isolated into independent services.
- ☁️ **AWS-Style Deployment (LocalStack)** — ECS, RDS, MSK, API Gateway simulations.
- 📨 **Kafka Messaging** — Event-driven inter-service communication.
- 🔗 **gRPC Support** — High-performance service-to-service transport.
- 🚪 **API Gateway** — Routing, load-balancing, filtering (Spring Cloud Gateway).
- 🔐 **Authentication Service** — JWT-based login & token verification.
- 🗄 **Dedicated Databases** — Each service uses its own PostgreSQL instance.
- 🐳 **Dockerized Everything** — Every service packaged as a container.
- 🧱 **Clean Architecture** — DTOs, Entities, Mappers, Repositories, Services.
- 📊 **Centralized Logging** — Structured logs (JSON-ready).
- 🧪 **Automated Testing** — Unit + integration support.

---

# 🧠 Tech Stack

| Layer                  | Technologies |
|------------------------|--------------|
| **Backend**            | Spring Boot, Spring Data JPA, Spring Security |
| **API Gateway**        | Spring Cloud Gateway |
| **Async Messaging**     | Apache Kafka / MSK (via LocalStack) |
| **Service-to-Service**  | REST + gRPC |
| **Databases**          | PostgreSQL (Dockerized) |
| **Containerization**   | Docker, Docker Compose |
| **Cloud Simulation**   | LocalStack (ECS, RDS, API Gateway, MSK) |
| **Authentication**     | JWT Tokens |
| **Build Tools**        | Maven |
| **Monitoring**         | Actuator |

---

# 🏗️ Microservices Overview

```
patient-management-system/
│
├── api-gateway/         # Entry point for all requests
├── auth-service/        # JWT authentication + user management
├── patient-service/     # Patient CRUD, validation, DTO mapping
├── appointment-service/ # Scheduling, doctor-patient allocation
├── notification-service/# Kafka consumers for emails/SMS
├── billing-service/     # Optional - medical billing, invoices
│
├── common-libs/         # Shared DTOs, utilities
│
└── deployment/
    ├── docker-compose.yml
    ├── localstack/
    └── infra/           # Infrastructure-as-Code

```

**Each microservice contains**:

```
controller/
dto/
entity/
mapper/
repository/
service/
config/
```

# 🗃️ Architecture Diagram (High-Level) :

## 📦 Deployment (LocalStack + Docker)

### ✔ Simulated AWS Services
```
Your LocalStack environment mimics real AWS services:

- **ECS** → Runs all microservice containers  
- **RDS** → PostgreSQL instances for each microservice  
- **MSK** → Kafka clusters for event-driven communication  
- **API Gateway** → Entry point for all external requests  
- **IAM** → Roles & permissions (simulated)
```
---

### 📁 Deployment Folder Contains

```
deployment/
│
├── docker-compose.yml # Orchestrates all microservices + Kafka + Postgres
├── localstack/ # Configuration for LocalStack AWS simulation
└── infra/ # Infrastructure-as-Code (IaC) for AWS-style setup

```

### ▶️ Run Entire System
```bash
docker-compose up --build
# Patient Service
```


---


## 🗄 Database Schema (High-Level ERD)

### **Patient Service**


patient(
id,
name,
email,
dob,
registered_at
)

### **Auth Service**
user(
id,
username,
password_hash,
roles
)

### **Appointment Service**
appointment(
id,
patient_id,
doctor_id,
date,
status
)

markdown
Copy code

### **Notification Service**
event_log(
id,
event_type,
payload
)


---

## 🔐 JWT Authentication Flow

1. **Client sends credentials**  
   `POST /auth/login` with *username & password*

2. **Auth service validates**  
   - Verifies user  
   - Generates a JWT token  
   - Returns it to the client

3. **Client calls any microservice**  
   Adds header:  
Authorization: Bearer <token>

4. **API Gateway intercepts**  
- Validates JWT  
- Extracts roles/claims  
- Rejects invalid/expired tokens

5. **Request forwarded**  
**Sent to the appropriate microservice (Patient, Appointment, etc.)**

---

## 📚 API Endpoints (Sample)

### **Patient Service**
```
GET /api/patients
POST /api/patients
GET /api/patients/{id}
PUT /api/patients/{id}
DELETE /api/patients/{id}
```


### **Auth Service**
```
POST /auth/register
POST /auth/login
```

### **Appointment Service**
```
POST /appointments
GET /appointments?patientId=
```

### **Notification Service** (Kafka-triggered)
```
POST /notify/email
```

---

## 🧮 Build & Run Instructions

### 🔹 Backend Microservices
```
mvn clean install
mvn spring-boot:run
```

### 🔹 Run with Docker
```
docker-compose up --build

```

### 🔹 LocalStack Setup (AWS Simulation)
```
awslocal s3 ls
awslocal ecs list-clusters
```

# ⚙️ Requirements

```
Java JDK 21+

Maven

Docker & Docker Compose

LocalStack

PostgreSQL
```

# 📄 License
MIT License
**This project is licensed under the MIT License. See the LICENSE file for details.**

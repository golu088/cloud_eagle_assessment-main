

---

# 🚀 GitHub Access Report System

![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.2.4-brightgreen.svg)
![Java](https://img.shields.io/badge/Java-17-blue.svg)
![WebFlux](https://img.shields.io/badge/Spring%20WebFlux-Reactive-blueviolet.svg)

> ⚡ A scalable, production-ready backend system designed to efficiently manage access insights across large GitHub organizations.

---

## 📌 Overview

The **GitHub Access Report System** is a robust backend service built using Spring Boot that integrates with the GitHub REST API to generate structured access reports for organizations.

It aggregates repository and collaborator data and transforms it into a **user-centric access model**, providing clear visibility into which users have access to which repositories.

The system is designed for **high performance, scalability, and maintainability**, making it suitable for enterprise-scale environments.

---

## 🎯 Problem Statement

Managing repository access across large organizations is complex and often lacks visibility.

This system solves the problem by:

* Aggregating repository and collaborator data
* Mapping users to repositories they can access
* Providing a clean REST API for access reporting

---

## ✨ Key Features

### ⚡ High Performance & Scalability

* Parallel data fetching using `CompletableFuture`
* Handles large datasets (100+ repositories, 1000+ users)

### 🔄 Reactive API Communication

* Uses Spring **WebClient (WebFlux)** for non-blocking API calls
* Improves performance in I/O-heavy operations

### 📄 Pagination Handling

* Efficient handling of GitHub API pagination (`per_page=100`)
* Ensures complete data retrieval

### 🧠 Intelligent Caching

* Integrated **Caffeine Cache** with `@Cacheable`
* Reduces redundant API calls and improves speed

### 🛡️ Robust Error Handling

* Centralized exception handling using `@ControllerAdvice`
* Handles:

  * `401 Unauthorized`
  * `403 Forbidden (Rate Limit)`
  * `404 Not Found`

### 🧩 Clean Architecture

```
controller/
service/
client/
model/
config/
```

---

## 🛠️ Tech Stack

| Category    | Technology                           |
| ----------- | ------------------------------------ |
| Language    | Java 17                              |
| Framework   | Spring Boot 3.2.4                    |
| Web Layer   | Spring MVC + WebFlux                 |
| HTTP Client | WebClient                            |
| Concurrency | CompletableFuture, ConcurrentHashMap |
| Caching     | Caffeine                             |
| Testing     | JUnit 5, Mockito                     |
| Build Tool  | Maven                                |

---

## 🏗️ System Flow

1. Authenticate using GitHub Personal Access Token (PAT)
2. Fetch all repositories of the organization
3. For each repository:

   * Fetch collaborators using parallel API calls
4. Transform data:

   * Convert **Repository → Users** into **User → Repositories**
5. Cache results for faster repeated access
6. Return structured JSON response via REST API

---

## ⚙️ Setup & Configuration

### 1️⃣ Prerequisites

* Java 17+
* Maven installed
* GitHub Personal Access Token (PAT)

Required scopes:

* `repo`
* `read:org`

---

### 2️⃣ Configuration

Update `application.yml`:

```yaml
github:
  token: ghp_YOUR_GITHUB_TOKEN
  org: your-organization-name
```

⚠️ Never commit your actual token to GitHub.

---

### 3️⃣ Build & Run

```bash
mvn clean install
mvn spring-boot:run
```

Application runs at:

```
http://localhost:8080
```

---

## 📡 API Usage

### 🔹 Endpoint

```
GET /access-report
```

---

### 📄 Sample Response

```json
{
  "octocat": [
    "Hello-World",
    "Spoon-Knife"
  ],
  "torvalds": [
    "linux",
    "git"
  ],
  "defunkt": [
    "github-services"
  ]
}
```

---

### 🔍 Response Format

* **Key** → GitHub username
* **Value** → List of repositories accessible by the user

---

## ⚠️ Rate Limiting Strategy

GitHub API rate limits (~5000 requests/hour) are handled by:

* Caching using Caffeine
* Efficient parallel API calls
* Minimizing redundant requests

Future improvement:

* Retry mechanism with exponential backoff

---

## 🧠 Design Decisions

* User-centric mapping for better readability
* Parallel execution to reduce response time
* Reactive WebClient for efficient I/O
* Caching layer for improved performance

---

## 📌 Assumptions

* GitHub token has required permissions
* Organization data is accessible
* Only active collaborators are included

---

## ⭐ Final Note

This project demonstrates:

* Scalable API integration
* Concurrency handling
* Performance optimization
* Clean backend architecture

It reflects real-world, production-level backend engineering practices.

---


# 🚀 GitHub Repository Access Analyzer

![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen.svg)
![Java](https://img.shields.io/badge/Java-17-blue.svg)
![WebFlux](https://img.shields.io/badge/WebFlux-Reactive-blueviolet.svg)

> ⚡ A scalable backend service that provides clear insights into repository access across GitHub organizations.

---

## 📌 Project Description

The **GitHub Repository Access Analyzer** is a backend system built using Spring Boot that connects with the GitHub API to analyze access control within an organization.

It collects repository and collaborator information and converts it into a **user-focused access report**, helping teams understand who has access to which repositories.

---

## 🎯 Objective

This project helps to:

* Retrieve all repositories of an organization
* Identify users with access to each repository
* Generate a structured report mapping users to repositories
* Provide this data via a REST API

---

## ✨ Features

### ⚡ Scalable & Fast

* Parallel API calls using `CompletableFuture`
* Supports large organizations (100+ repos, 1000+ users)

### 🔄 Reactive API Calls

* Uses Spring WebClient (non-blocking)
* Better performance for network operations

### 📄 Pagination Handling

* Uses `per_page=100` to fetch complete data

### 🧠 Caching

* Caffeine Cache integration
* Reduces repeated API calls

### 🛡️ Error Handling

* Global exception handling
* Handles 401, 403, 404 errors

---

## 🛠️ Tech Stack

* Java 17
* Spring Boot
* Spring WebFlux
* WebClient
* CompletableFuture
* Caffeine Cache
* Maven

---

## 🏗️ System Flow

1. Authenticate using GitHub Token
2. Fetch organization repositories
3. Fetch collaborators for each repo
4. Convert data into user → repositories mapping
5. Cache results
6. Return JSON response via API

---

## ⚙️ Setup

### 🔹 Prerequisites

* Java 17+
* Maven
* GitHub Personal Access Token

Required permissions:

* repo
* read:org

---

### 🔹 Configuration

Update `application.yml`:

```yaml
github:
  token: YOUR_TOKEN
  org: YOUR_ORG_NAME
```

---

### 🔹 Run Project

```bash
mvn clean install
mvn spring-boot:run
```

App runs on:

```
http://localhost:8080
```

---

## 📡 API Endpoint

### GET Access Report

```
GET /access-report
```

---

## 📄 Sample Response

```json
{
  "userA": ["repo1", "repo2"],
  "userB": ["repo2"],
  "userC": ["repo3"]
}
```

---

## ⚠️ Rate Limit Handling

* Caching used to reduce API calls
* Parallel execution improves efficiency

---

## 🧠 Design Decisions

* User-based mapping for clarity
* Parallel execution for speed
* Reactive API calls for performance
* Caching for optimization

---

## 📌 Assumptions

* Valid GitHub token provided
* Organization is accessible
* Only active collaborators included

---

## ⭐ Conclusion

This project demonstrates:

* API integration with GitHub
* Scalable backend design
* Concurrency handling
* Clean and maintainable code

---

💻 Built for learning and real-world backend practice.

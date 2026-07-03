# Sales Kafka - Saga Patterns
Monorepo of a project implementing saga patterns with Java Spring Boot and Kafka.

[![Java](https://img.shields.io/badge/Java-21-339933?logo=openjdk&logoColor=white)](https://openjdk.org/)
[![Spring Boot](https://img.shields.io/badge/Spring_Boot-3.5-6DB33F?logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![Gradle](https://img.shields.io/badge/Gradle-9.6-02303A?logo=gradle&logoColor=white)](https://gradle.org/)
[![Apache Kafka](https://img.shields.io/badge/Apache_Kafka-231F20?logo=apachekafka&logoColor=white)](https://kafka.apache.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![MongoDB](https://img.shields.io/badge/MongoDB-47A248?logo=mongodb&logoColor=white)](https://www.mongodb.com/)
[![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)
[![Redpanda Console](https://img.shields.io/badge/Redpanda_Console-AE1C28?logo=foodpanda&logoColor=white)](https://github.com/redpanda-data/console)

## Technologies
* **Java 21**
* **Spring Boot 3.5**
* **Gradle 9.6**
* **Apache Kafka**
* **API REST**
* **PostgreSQL**
* **MongoDB**
* **Docker**
* **Redpanda Console**

# Orchestrated Saga Architecture
<img width="1736" height="906" alt="image" src="https://github.com/user-attachments/assets/5766797f-f1e4-45f3-993a-d52832cf210f" />


* **Order-Service**: microservice responsible only for generating an initial request and receiving a notification. Here we have REST endpoints to start the process and retrieve event data. The database used will be MongoDB.
* **Product-Validation-Service**: microservice responsible for validating whether the product specified in the order exists and is valid. This microservice will store a product validation for an order ID. The database used will be PostgreSQL.
* **Payment-Service**: microservice responsible for making a payment based on the unit values ​​and quantities informed in the order. This microservice will store the payment information for an order. The database used will be PostgreSQL.
* **Inventory-Service**: microservice responsible for lowering the stock of products from an order. This microservice will store the download information of a product for an order ID. The database used will be PostgreSQL.

**All services will go up through **docker-compose.yml**.**

# Topic Mapping

| Service                    | Kafka Topic                 | Type               |
|----------------------------|-----------------------------|--------------------|
| order-service              | start-saga                  | consumer           |
| product-validation-service | product-validation-success  | consumer           |
| product-validation-service | product-validation-fail     | consumer           |
| payment-service            | payment-success             | consumer           |
| payment-service            | payment-fail                | consumer           |
| inventory-service          | inventory-success           | consumer           |
| inventory-service          | inventory-fail              | consumer           |
| inventory-service          | notify-ending               | producer           |

# How to run
There are several ways to run:
1. Running everything via `docker-compose`
2. Running everything through the automation `script` that i made available (`build-bash.sh`)
3. Running only the database and message broker (Kafka) services separately
4. Running applications manually via CLI (`java -jar` or `gradle bootRun` or via IntelliJ)

To run the applications, you will need to have installed:

* **Docker**
* **Java 21**
* **Gradle 9.6**


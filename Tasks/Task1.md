# Task 1 - Project Setup and Environment Configuration

## Objective

Prepare the development environments for the Midas Core system and verify that the project can build and run successfully

## Background

Midas Core is responsible for receiving, validating, and recording financial transactions.

The system interacts:

- Kafka for receiving transaction data
- SQL Database for storing and validating records
- REST APIs for exposing processed information

The project is built using Spring Boot and follows a pre-defined architecture scaffold.

## Technologies Introduced

- Java 17
- Spring Boot
- Maven
- APache Kafka
- H2 Database
- REST APIs
- JPA (Java Persisitence API)
- IntelliJ IDEA

## Implementation Plan

### Step 1: Repository Setup

- Fork the farage-midas repo
- Clone it locally
- Open the project in IntelliJ IDEA

### Step 2: Java Environment Setup

- Install Java 17
- Verify installation using:

`java -version`

- Configure IntelliJ to use Java 17

### Step 3: Explore Project Structure

## Maven Wrapper (.mvn/wrapper)

The Maven Wrapper allows a project to use a specific Maven version without requiring Maven to be pre-installed on a developer's machine.

Benefits:
- Ensures all developers use the same Maven version
- Improves build consistency
- Simplifies project setup
- Reduces environment-related issues

## src

### Componenet

  ### DatabaseConduit
  
  Purpose:
  Acts as an intermediary between the application logic and the database layer.

### Entity (represents data stored in a database)

  ### UserRecord Entity
  
  Purpose:
  Represents a user stored in the database.

### Foundation (data transfer objects)

  ### Balance.java
  
  Purpose
  
  `Balance` is a simple Java object used to represent balance information when exchanging data between services or APIs. 

  ### Transaction.java

  Purpose
  
  `Transaction` represents a money transfer between two users.
  
  It contains information about:
  
  - The sender of the transaction
  - The recipient of the transaction
  - The amount being transferred

### Repository

  ### UserRepository.java
  
  Purpose
  
  `UserRepository` provides database access for `UserRecord` entities.
  
  It acts as the communication layer between the application and the database.

### MidasCoreApplication.java

Purpose

`MidasCoreApplication` is the main entry point of the Midas Core system.
It starts the Spring Boot application and initializes all required components.

### Test

  ### TaskOneTests

  Purpose
  
  TaskOneTests is the introductory verification test for the Midas Core project. Its purpose is to ensure that the Spring Boot    application starts successfully and that the application context loads without any configuration or dependency issues.





  







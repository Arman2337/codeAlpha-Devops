# Task 3: Java Application using Gradle

## Overview
This project demonstrates how to automate Java project builds using Gradle. It covers dependency management and integrates a CI/CD pipeline using GitHub Actions to continuously build and test the application.

## Prerequisites
- Java Development Kit (JDK) 17 or higher installed.
- Gradle installed (or you can use the Gradle Wrapper, though not included by default here to keep things simple).

## Setup Instructions

### 1. Build the Project
To compile the Java source code, run:
```bash
.\gradlew build
```
This command automatically downloads the dependencies defined in `build.gradle`, compiles the code, runs the tests, and packages the application.

### 2. Run the Application
To execute the main method of the application:
```bash
.\gradlew run
```
You should see the output: `Hello from Gradle-managed Java App!`

### 3. Run Tests
To execute the unit tests using JUnit:
```bash
.\gradlew test
```

## Dependency Management
Look at `build.gradle`. Under the `dependencies` block, you will see `implementation 'com.google.guava:guava:32.1.3-jre'`. 
Gradle resolves this from the Maven Central repository. This eliminates the need to manually download and bundle `.jar` files.

## Continuous Integration (CI/CD)
This project includes a `.github/workflows/ci.yml` file. If you push this repository to GitHub, GitHub Actions will automatically:
1. Provision a Linux virtual machine.
2. Checkout the code.
3. Install JDK 17.
4. Execute `gradle build`.

This ensures that every commit is automatically verified, which is a core DevOps principle for continuous delivery.

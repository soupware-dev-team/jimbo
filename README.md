# Jimbo: System Monitoring Utility

## Introduction

Jimbo is an enterprise-grade, lightweight command-line interface (CLI) utility, meticulously crafted in Golang. This utility is designed to provision real-time analytics of system vitals. The architecture is focused on performance, scalability, and extensible functionality. This document serves as a comprehensive guide for developers, system administrators, and anyone else interested. Last updated on September 2023.
## Table of Contents

1. [Introduction](#Introduction)
2. [Command Taxonomy and Parameter Definitions](#Command-Taxonomy-and-Parameter-Definitions)
4. [Background Operation & Graceful Termination](#Background-Operation-Graceful-Termination)
5. [Command Overview](#Command-Overview)
6. [Optimizations Overview](#Optimizations-Overview)
7. [Coding Conventions & Naming Schema](#Coding-Conventions-Naming-Schema)
8. [Prescribed Development Practices](#Prescribed-Development-Practices)
9. [Version Control and Collaboration](#Version-Control-and-Collaboration)
10. [Testing Methodologies](#Testing-Methodologies)
11. [CI/CD Pipelines](#CI-CD-Pipelines)
12. [Git Branching Strategy](#Git-Branching-Strategy)
13. [Vulnerability Reporting](#Vulnerability-Reporting)
14. [Terminology Glossary](#Terminology-Glossary)
## 1. Command Taxonomy and Parameter Definitions

- **CPU Metrics**
    - Command: `jimbo cpu`
    - Parameters: `--json`, `--xml`, `--plain`

- **Memory Analytics**
    - Command: `jimbo mem`
    - Parameters: `--json`, `--xml`, `--plain`

- **Disk Utilization**
    - Command: `jimbo disk`
    - Parameters: `--json`, `--xml`, `--plain`

- **Network Metrics**
    - Command: `jimbo net`
    - Parameters: `--json`, `--xml`, `--plain`

- **Process Information**
    - Command: `jimbo proc`
    - Parameters: `--json`, `--xml`, `--plain`, `--pid "PID"`

- **Command History**
    - Command: `jimbo history`
    - Purpose: Enumerates past commands in multiples of 5 (e.g., 5, 10, 15, ...)

- **Documentation & Help**
    - Command: `jimbo help`
    - Sub-Help Menus: `jimbo cpu --help`, `jimbo mem --help`, etc.

- **Process Query**
    - Command: `jimbo search`
    - Parameters: `--pid "PID", --name "Process Name"

- **Logging & Debugging**
    - Command: `jimbo logs`
    - Parameters: `--enable-debug`, `--disable-debug`   

- **System Threads**
    - Command: `jimbo threads`
    - Parameters: `--json`, `--xml`, `--plain`
 
- **System Services**
    - Command: `jimbo services`
    - Parameters: `--json`, `--xml`, `--plain`, `--state=<state>`

- **Holistic System Overview**
    - Command: `jimbo overview`
    - Parameters: `--json`, `--xml`, `--plain`

- **Configuration & Alerting**
    - Command: `jimbo cfg/config`
    - Parameters: `--set-alert=<metric>:<threshold>`, `--remove-alert=<metric>`

- **Software Version Information**
    - Command: `jimbo ver/version`

**Common Parameters**:
    - `--json`, `--xml`, `--plain`: Output format selectors.
    - `--pid "PID"`: Process Identification Parameter.
    - `--enable-debug`, `--disable-debug`: Debugging toggle.
## 2. Background Operation & Graceful Termination

Jimbo offers seamless background operation and minimizes to the system tray when the 'X' button is pressed or when `jimbo &` is typed in the console. For graceful termination, input `:wq` in the CLI.
## 3. Command Overview

#### 1. "jimbo cpu" Command

The `jimbo cpu` command furnishes real-time and historical data on CPU utilization. This is invaluable for diagnosing bottlenecks in system performance.

- **Parameters**:
    - `--json`: Output in JSON format.
    - `--xml`: Output in XML format.
    - `--plain`: Plain text output.

#### 2. "jimbo mem" Command

The `jimbo mem` command provides crucial insights into memory usage, including but not limited to RAM, swap memory, and cache statistics.

- **Parameters**:
    - `--json`, `--xml`, `--plain`: Choose the output format.

#### 3. "jimbo disk" Command

Gives an account of disk utilization, which is essential for understanding how storage resources are being consumed.

- **Parameters**:
    - `--json`, `--xml`, `--plain`: Choose the output format.

#### 4. "jimbo net" Command

Offers granular metrics on network utilization, including bandwidth usage, latency, and packet statistics.

- **Parameters**:
    - `--json`, `--xml`, `--plain`: Choose the output format.

#### 5. "jimbo proc" Command

Displays detailed information about running processes, which is critical for system monitoring and debugging.

- **Parameters**:
    - `--json`, `--xml`, `--plain`: Choose the output format.
    - `--pid "PID"`: Filter by a specific Process ID.

#### 6. "jimbo history" Command

Enumerates past commands in multiples of 5. Essential for auditing and understanding past actions.

#### 7. "jimbo help" Command

Provides a help menu and additional sub-help menus for each command. This is the go-to for understanding how each command and parameter functions.

#### 8. "jimbo search" Command

Allows querying of specific processes either by their Process ID or name. Useful for quick lookups.

- **Parameters**:
    - `--pid "PID"`: Search by Process ID.
    - `--name "Process Name"`: Search by process name.

#### 9. "jimbo logs" Command

Enables or disables debugging, which is crucial for development and troubleshooting.

- **Parameters**:
    - `--enable-debug`: Enable debugging.
    - `--disable-debug`: Disable debugging.

#### 10. "jimbo threads" Command

Provides intricate details about system threads, invaluable for diagnosing issues related to concurrency and parallelism.

- **Parameters**:
    - `--json`, `--xml`, `--plain`: Choose the output format.

#### 11. "jimbo services" Command

Offers a comprehensive overview of system services, enabling users to understand which services are active, inactive, or failed.

- **Parameters**:
    - `--json`, `--xml`, `--plain`: Choose the output format.
    - `--state=<state>`: Filter by service state (e.g., running, stopped).

## 4. Optimizations Overview

Jimbo leverages a plethora of best practices to optimize performance, resource utilization, and type safety.

```
Lazy Initialization: Resources are allocated only when needed to minimize startup time and memory footprint.
```
```
Concurrency: GoLang's goroutines and channels are leveraged for asynchronous operations, enhancing CPU utilization.
```
```
Resource Pooling: Reusable resources like database connections are pooled to avoid the overhead of frequent allocation and deallocation.
```
 ```
Data Structures: Efficient data structures like hash maps are used for quick look-up operations.
```
```
Caching: Frequent queries and non-mutable objects are cached to reduce IO operations.
```
```
Avoiding Global Variables: This practice helps in reducing side-effects and makes the code more maintainable and testable. 
```
```
Loop Unrolling and Tail Recursion: These are used in performance-critical sections to reduce the overhead of loop control and function calls. 
```
```
Just-In-Time Compilation: Transforms interpreted code into compiled code during runtime, reducing the execution time.
```
```
Batch Processing: Processes data in bulk rather than individually to minimize the CPU load.
```
```
Memory Mapped Files: Used for quicker file I/O operations, especially beneficial for large files.
```
```
Connection Multiplexing: Allows multiple logical connections to be multiplexed over a single physical connection, reducing the overhead of TCP connection establishment and termination.
```
```
Data Compression: Employs algorithms like Gzip for data compression, reducing network and storage overhead.
```
```
Algorithmic Complexity: Prioritizes algorithms with lower time complexity for data manipulation tasks.
```
```
Throttling: Limits the number of simultaneous connections or requests to avoid overwhelming system resources.
```
```
Database Indexing: Employs indexing techniques to accelerate database queries.
```
```
Immutable Data Structures: Uses immutable data structures to minimize lock contention in multi-threaded environments.
```
```
Code Vectorization - Takes advantage of SIMD (Single Instruction, Multiple Data) CPU instructions for data parallelism.
```
## 5.  Coding Conventions & Naming Schema

Adherence to Go's idiomatic coding conventions is imperative. Variables and function nomenclature should be both descriptive and concise. Constants shall be denominated in uppercase, and package names in lowercase, to maintain uniformity across the codebase.
## 6. Prescribed Development Practices

Code modularity, readability, and maintainability are non-negotiable standards. Comprehensive unit tests must accompany each functional component. All code alterations necessitate peer reviews by two team members. In-code comments and documentation should elucidate not just the 'what', but pivotally, the 'why'.
## 7. Version Control and Collaboration

### Git Workflow
- **Fork the Repository**: Developers should start by forking the main repository to their own GitHub account.
- **Clone the Forked Repository**: Clone the repository to your local machine for development.

        git clone https://github.com/<YourUsername>/jimbo.git

- **Add Upstream Remote**: Add the main repository as an upstream remote to keep your local repository updated.

        git remote add upstream https://github.com/soupware-development-team/jimbo.git

- **Fetching Updates**: Periodically fetch updates from the main repository.

        git fetch upstream
        git merge upstream/main

### Feature Branches
- Always create a new branch for each feature/bugfix/hotfix/etc. 

        git checkout -b feature/new-feature

- **Commit Often**: Make granular and meaningful commits.

        git add .
        git commit -m "detailed commit message"

- **Push to Origin**: Push your changes to your fork.

        git push origin feature/new-feature
### Git Branching Strategy

To manage the complexity of development and streamline the flow of changes in Jimbo, we adhere to a specific branching strategy. Here's a breakdown:
#### `prod` (Production Branch)

- **Purpose**: This branch represents the codebase currently in production.
- **Who Can Merge**: Only senior developers and DevOps engineers.

#### `dev` (Development Branch)

- **Purpose**: The bleeding-edge code. All new features and bug fixes are merged into this branch.
- **Who Can Merge**: Developers and lead developers.

#### `feature/` (Feature Branches)

- **Naming Convention**: `feature/<feature-name>`
- **Purpose**: For new features. Each new feature should reside in its own branch.
- **Who Can Merge**: Developers, after a successful code review.

#### `bugfix/` (Bugfix Branches)

- **Naming Convention**: `bugfix/<bug-name>`
- **Purpose**: To fix bugs in the `dev` branch. Once fixed, they will be merged back into `dev`.
- **Who Can Merge**: Developers, after a successful code review.

#### `hotfix/` (Hotfix Branches)

- **Naming Convention**: `hotfix/<issue-name>`
- **Purpose**: To quickly patch production releases. These branches are based on `prod` and are merged back into both `prod` and `dev`.
- **Who Can Merge**: Only senior developers and DevOps engineers, after rigorous testing.

By following these branching conventions, we aim to keep Jimbo's development process organized, predictable, and scalable, thereby ensuring high-quality code that meets the rigorous standards of an enterprise-grade system monitoring utility.
## 9. Pull Requests (PRs)
- Make sure your branch is updated with the latest changes from the main repository.
- Create a pull request from your fork to the main repository.
- Fill in the PR template detailing what the PR is aiming to solve or add.
- Wait for the code review and address any comments or suggestions.
- Once approved, the PR will be merged into the main repository.
### Code Reviews
- Peer code reviews are mandatory for every PR.
- Use GitHub's review features to comment and approve or request changes.
- The focus should be on code quality, functionality, and adherence to project guidelines.
#### How to review code
 1. **Security**
    - **Input Validation**: To prevent SQL injection, XSS, etc.
    - **Dependencies**: Scan for secure libraries.
    - **Data Protection**: Ensure encryption or hashing.
      
2. **Performance**
    - **Time Complexity**: Optimize algorithms.
    - **Memory Usage**: Check for memory leaks.
      
3. **Readability**
    - **Naming**: Ensure meaningful variable and function names.
    - **Structure**: Look for clean, modular code.
      
4. **Documentation**
    - **Comments**: Ensure code is well-commented, explaining the 'how' and 'why'

## 10. Testing Methodologies

To ensure Jimbo's reliability and robustness, the following testing methodologies will be employed:

### Unit Testing

- **Purpose**: To validate the correctness of individual units of source code.
- **Tools**: Go's native `testing` package.
- **Scope**: Each Go module will have corresponding test files.

### Integration Testing

- **Purpose**: To validate the interactions between integrated components.
- **Tools**: `Testify` for Go-based assertions, and `httpmock` for mocking HTTP requests.
- **Scope**: Focus on module-to-module interactions, especially critical paths like data ingestion and alerting.

### End-to-End Testing

- **Purpose**: To validate the system as a whole, in an environment that mimics real-world use cases.
- **Tools**: Selenium for UI testing, Postman for API testing.
- **Scope**: Entire workflow from system startup to graceful termination.

### Performance Testing

- **Purpose**: To ensure the system performs well under the load of many users.
- **Tools**: `JMeter` for load testing, `Grafana` for monitoring.
- **Scope**: Focus on CPU, memory, and network utilization.

### Security Testing

- **Purpose**: To identify vulnerabilities in the system.
- **Tools**: OWASP ZAP for penetration testing, Snyk for dependency scanning.
- **Scope**: All exposed interfaces and dependencies.
## 11. CI/CD Pipelines

To maintain a streamlined and efficient development process, a CI/CD (Continuous Integration/Continuous Deployment) pipeline will be implemented.

### Continuous Integration

1. **Version Control**: Git with feature branching strategy.
2. **Automated Builds**: `Go Build` for compilation.
3. **Automated Testing**: All the tests mentioned in the Testing Methodologies will be automated using `Go Test`.
4. **Code Quality**: Static code analysis using `golint` and `go vet`.
5. **Security Scanning**: Snyk for dependency security checks.

### Continuous Deployment

1. **Environment Setup**: Separate environments for development, staging, and production.
2. **Configuration Management**: Environment variables for different configurations.
3. **Automated Deployments**: Using Kubernetes for orchestration.
4. **Rollbacks**: Automatic rollbacks in case of deployment failure.
5. **Monitoring and Alerts**: Prometheus for monitoring, integrated with Slack for real-time alerts.
## 12.  Vulnerability Reporting

To responsibly disclose security vulnerabilities, please send a detailed report to jimbo@soupware.xyz The report should include steps to reproduce the vulnerability and any potential impact. Do NOT disclose the vulnerability publicly before it has been responsibly handled by the maintainers.

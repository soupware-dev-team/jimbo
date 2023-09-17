# Jimbo: System Monitoring Utility

## Introduction

Jimbo is an enterprise-grade, lightweight command-line interface (CLI) utility, meticulously crafted in GoLang, designed to provision both real-time and static analytics of system vitals. The utility encapsulates a robust architecture focused on performance, scalability, and extensible functionality. This document delineates the project's command taxonomy, feature spectrum, and prescribes best practices for an agile development lifecycle.
## Table of Contents

1. Command Taxonomy and Parameter Definitions
2. Extended Command Suite & Parameterization
3. Background Operation & Graceful Termination
4. Unix-Inspired Command-Line Interface
5. Native Alert Notifications via Windows API
7. Coding Conventions & Naming Schema
8. Prescribed Development Practices
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
    - Parameters: `--pid "PID", --name "Process Name"`

- **Logging & Debugging**
    - Command: `jimbo logs`
    - Parameters: `--enable-debug`, `--disable-debug`
## 2. Extended Command Suite & Parameterization

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
## 3. Background Operation & Graceful Termination

Jimbo possesses the capability to operate inconspicuously in the background, minimizing to the system tray upon interaction with the 'X' button. 
Graceful termination can be initiated by entering `:wq` in the CLI.
## 4. Unix-Inspired Command-Line Interface

To provide a familiar interaction paradigm, the CLI emulates a Unix-like interface, prefacing each command with `root@jimbo:~$ `.
## 5. Native Alert Notifications via Windows API

Leveraging native Windows API, Jimbo orchestrates real-time alert notifications for system vitals, optimizing for immediate user responsiveness.
## 6. Version Control Strategy

A robust version control strategy will be executed using Git. Feature-specific branches will be instantiated from the mainline, and upon completion, subjected to rigorous code reviews prior to merging. Semantic versioning will be employed to maintain a coherent release timeline.

## 7. Coding Conventions & Naming Schema

Adherence to GoLang's idiomatic coding conventions is imperative. Variables and function nomenclature should be both descriptive and concise. Constants shall be denominated in uppercase, and package names in lowercase, to maintain uniformity across the codebase.

## 8. Prescribed Development Practices

Code modularity, readability, and maintainability are non-negotiable standards. Comprehensive unit tests must accompany each functional component. All code alterations necessitate peer reviews. In-code comments and documentation should elucidate not just the 'what', but pivotally, the 'why'.
## 9. Version Control and Collaboration

### Git Workflow
- **Fork the Repository**: Developers should start by forking the main repository to their own GitHub account.
- **Clone the Forked Repository**: Clone the repository to your local machine for development.

        git clone https://github.com/<YourUsername>/jimbo.git

- **Add Upstream Remote**: Add the main repository as an upstream remote to keep your local repository updated.

        git remote add upstream https://github.com/ferrislovescpp/jimbo.git

- **Fetching Updates**: Periodically fetch updates from the main repository.

        git fetch upstream
        git merge upstream/main

### Feature Branches
- Always create a new branch for each feature or bugfix. 

        git checkout -b feature/new-feature

- **Commit Often**: Make granular and meaningful commits.

        git add .
        git commit -m "detailed commit message"

- **Push to Origin**: Push your changes to your fork.

        git push origin feature/new-feature
### Pull Requests (PRs)
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

### Vulnerability Reporting

To responsibly disclose security vulnerabilities, please send a detailed report to jimbo@deusexstudios.com. The report should include steps to reproduce the vulnerability and any potential impact. Do NOT disclose the vulnerability publicly before it has been responsibly handled by the maintainers.

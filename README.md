# Jimbo: System Monitoring Utility

## Introduction

Jimbo is an enterprise-grade, lightweight command-line interface (CLI) utility, meticulously crafted in GoLang, designed to provision both real-time and static analytics of system vitals. The utility encapsulates a robust architecture focused on performance, scalability, and extensible functionality. This document delineates the project's command taxonomy, feature spectrum, and prescribes best practices for an agile development lifecycle.

## Table of Contents

1. Command Taxonomy and Parameter Definitions

2. Extended Command Suite & Parameterization

3. Background Operation & Graceful Termination

4. Unix-Inspired Command-Line Interface

5. Native Alert Notifications via Windows API

6. Version Control Strategy

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

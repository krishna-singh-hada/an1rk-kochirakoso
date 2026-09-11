# 01 — Introduction to Containerization

## Introduction

**Containerization** packages an application together with its dependencies into a single portable unit.

It helps the same application run consistently across different environments.

## Core Concept

```text
Application Code
      ↓
Dependencies
Libraries, files, configs
      ↓
Container
Packaged application unit
      ↓
Container Runtime
Runs isolated applications
      ↓
Host System
Provides operating environment
```

## Flowchart Terms

| Term                  | Explanation                   |
| --------------------- | ----------------------------- |
| **Application Code**  | Main program being packaged   |
| **Dependencies**      | Required libraries and files  |
| **Container**         | Packaged application unit     |
| **Container Runtime** | Software that runs containers |
| **Host System**       | Machine running containers    |

## Why Containerization?

| Benefit         | Explanation                       |
| --------------- | --------------------------------- |
| **Consistency** | Same environment everywhere       |
| **Portability** | Move applications between systems |
| **Isolation**   | Separate application processes    |
| **Lightweight** | Uses fewer system resources       |
| **Scalability** | Starts containers quickly         |
| **Efficiency**  | Uses CPU and RAM efficiently      |
| **Agility**     | Speeds development and releases   |

## Containerization Mental Model

```text
Application
     ↓
Code + Dependencies
     ↓
Packaged Container
     ↓
Same Runtime Environment
     ↓
Development → Testing → Production
```

**Main idea:** Containerization reduces environment differences by packaging the application with what it needs to run.

## Key Terms

| Term                 | Meaning                                 |
| -------------------- | --------------------------------------- |
| **Containerization** | Packaging application with dependencies |
| **Runtime**          | Software that runs containers           |
| **Consistency**      | Same environment across stages          |
| **Portability**      | Easy movement between systems           |
| **Isolation**        | Separate processes from others          |
| **Lightweight**      | Lower resource usage                    |
| **Scalability**      | Quickly increase running instances      |
| **Efficiency**       | Better resource utilization             |
| **Agility**          | Faster development and deployment       |

## Key Takeaway

```text
Containerization
      ↓
Application + Dependencies
      ↓
Portable Container
      ↓
Consistent Execution
```

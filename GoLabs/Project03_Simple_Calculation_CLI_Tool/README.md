# Simple Calculation CLI Tool Project

## Table of Contents
1. [Overview](#overview)
2. [Fields Focus](#fields-focus)
3. [Key Concept Coverage](#key-concept-coverage)
4. [Project Requirements](#project-requirements)
5. [Project Constraints](#project-constraints)
6. [Implementation Steps](#implementation-steps)
7. [Sample Usage](#sample-usage)
8. [Learning Resources](#learning-resources)

## Overview
This project is about building a Command Line Interface (CLI) tool in Go that performs basic arithmetic operations like addition, subtraction, multiplication, and division. It serves as an exercise to deepen understanding of Go's syntax, functions, and packages, and introduces the concept of building CLI tools that can be containerized for consistent execution environments.

## Fields Focus
- **Backend Development**: Crafting the logic for arithmetic operations and user interaction through the CLI.
- **DevOps**: Containerizing the CLI tool using Docker for easy distribution and deployment.

## Key Concept Coverage
- **Functions and Packages**: Structuring the calculator's functionality into separate functions and organizing them within packages.
- **Go's Syntax and Basic Constructs**: Utilizing Go's syntax for variable declarations, control structures, and input/output operations.

## Project Requirements
- Go installed on your development machine.
- Basic understanding of arithmetic operations.
- Familiarity with command-line interfaces and Docker (for containerization).

## Project Constraints
- The CLI tool should validate input to ensure only numeric values are processed.
- Provide clear error messages for invalid inputs or unsupported operations.
- The tool should be stateless, processing provided inputs in one execution without storing any state between runs.

## Implementation Steps

### 1. **Environment Setup**
   - Ensure Go is installed:
     ```bash
     go version
     ```
   - Create your project directory and navigate into it:
     ```bash
     mkdir simple-calc && cd simple-calc
     ```

### 2. **Initialize Go Module**
   - Set up your Go module:
     ```bash
     go mod init simple-calc
     ```

### 3. **Design CLI Interface**
   - Decide on the CLI commands and flags. For example, to add two numbers:
     ```bash
     simple-calc add --num1 5 --num2 3
     ```

### 4. **Implement Arithmetic Functions**
   - Create functions for each operation (add, subtract, multiply, divide) in a separate package, e.g., `calc`:
     ```go
     // in calc/calc.go
     package calc

     func Add(num1, num2 float64) float64 {
       return num1 + num2
     }
     ```

### 5. **Parse Command-Line Arguments**
   - Use the `flag` package to parse command-line flags for operations and operands. Set up flags within your `main.go`:
     ```go
     import (
       "flag"
       "fmt"
       "simple-calc/calc"
     )

     func main() {
       num1 := flag.Float64("num1", 0, "First number")
       num2 := flag.Float64("num2", 0, "Second number")
       operation := flag.String("operation", "add", "Operation to perform")
       flag.Parse()

       // Example operation handling
       switch *operation {
         case "add":
           result := calc.Add(*num1, *num2)
           fmt.Printf("Result: %v\n", result)
         // Handle other operations
       }
     }
     ```

### 6. **Error Handling and Validation**
   - Ensure input validation and error handling for unsupported operations or invalid inputs.

### 7. **Testing**
   - Write tests for your arithmetic functions to ensure accuracy.
     ```bash
     go test ./calc...
     ```

### 8. **Compile the Program**
   - Build your CLI tool into an executable:
     ```bash
     go build -o simple-calc .
     ```

### 9. **Containerization with Docker**
   - Create a `Dockerfile` to containerize your application:
     ```Dockerfile
     FROM golang:alpine AS builder
     WORKDIR /app
     COPY . .
     RUN go build -o simple-calc .

     FROM alpine:latest  
     WORKDIR /root/
     COPY --from=builder /app/simple-calc .
     ENTRYPOINT ["./simple-calc"]
     ```
   - Build your Docker image:
     ```bash
     docker build -t simple-calc .
     ```

### 10. **Run Locally**
   - Test your CLI tool:
     ```bash
     ./simple-calc --operation add --num1 5 --num2 3
     ```

### 11. **Run with Docker**
   - Execute your tool within a Docker container:
     ```bash
     docker run simple-calc --operation add --num1 5 --num2 3
     ```

### 12. **Deployment**
   - If desired, push your Docker image to a container registry like Docker Hub for sharing:
     ```bash
     docker tag simple-calc yourusername/simple-calc
     docker push yourusername/simple-calc
     ```
## Sample Usage

After building the CLI tool, you can perform basic arithmetic operations by running commands in your terminal. Here are some examples of how to use the tool:

### Addition
```bash
./simple-calc --operation add --num1 5 --num2 3
# Output: Result: 8
```
### Subtraction
```bash
./simple-calc --operation subtract --num1 10 --num2 4
# Output: Result: 6
```
### Multiplication
```bash
./simple-calc --operation multiply --num1 6 --num2 7
# Output: Result: 42
```
### Division
```bash
./simple-calc --operation divide --num1 8 --num2 2
# Output: Result: 4
```

## Learning Resources

To enhance your understanding of the concepts and technologies used in this project, consider exploring the following resources:

- **Go Programming:**
  - [A Tour of Go](https://tour.golang.org/welcome/1): An interactive introduction to Go, covering the basics to more advanced topics.
  - [Effective Go](https://golang.org/doc/effective_go): Offers insights into writing clear, idiomatic Go code.

- **CLI Development in Go:**
  - [Building Command Line Applications in Go](https://www.youtube.com/watch?v=NOCElcMcFik): A video tutorial that walks through the process of creating CLI applications using Go.

- **Testing in Go:**
  - [Go Testing](https://golang.org/pkg/testing/): The official documentation for Go's testing package, providing guidelines for writing and running tests.

- **Docker and Containerization:**
  - [Docker Get Started](https://www.docker.com/get-started): The official starting guide for Docker, explaining the basics of containerization.
  - [Dockerizing a Go Application](https://www.callicoder.com/docker-golang-image-container-example/): A practical guide to containerizing Go applications with Docker.

- **Understanding Git and GitHub:**
  - [Git Handbook](https://guides.github.com/introduction/git-handbook/): A comprehensive guide to understanding and using Git and GitHub for version control.

- **RESTful Services in Go:**
  - [Creating Web Services with Go](https://www.youtube.com/watch?v=2v11Ym6Ct9Q): This tutorial covers how to build RESTful services in Go.

- **Go Modules:**
  - [Using Go Modules](https://blog.golang.org/using-go-modules): A blog post explaining how to work with Go modules for dependency management.

These resources provide a solid foundation for not only completing this project but also for future Go projects, deepening your knowledge in Go programming, web development, and software best practices.




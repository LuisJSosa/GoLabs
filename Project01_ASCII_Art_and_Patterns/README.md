# ASCII Art & Patterns Project

## Table of Contents
1. [Overview](#overview)
2. [Fields Focus](#fields-focus)
3. [Key Concept Coverage](#key-concept-coverage)
4. [Project Requirements](#project-requirements)
5. [Project Constraints](#project-constraints)
6. [Implementation Steps](#implementation-steps)
7. [Sample Output](#sample-output)
8. [Learning Resources](#learning-resources)

## Overview
This project involves developing a web service that dynamically generates ASCII art from user-provided text or patterns. The primary goal is to familiarize learners with Go's syntax, basic constructs, and control flow by creating a practical, backend-driven application. Additionally, this project serves as an introduction to deploying web applications to the cloud, emphasizing backend development and cloud computing fields.

## Fields Focus
- **Backend Development**: You will create server-side logic to convert input text into ASCII art, focusing on request handling, data processing, and response generation.
- **Cloud Computing**: The project will be deployed to a cloud platform, such as Heroku or AWS, to be accessible over the internet, introducing you to basic cloud services and deployment processes.

## Key Concept Coverage
- **Go's Syntax and Basic Constructs**: Learn how to set up a Go project, define variables, and use standard libraries.
- **Control Flow**: Explore how to use loops and conditional statements to manipulate data and generate ASCII art based on different criteria.

## Project Requirements
- Install Go (version 1.15 or later recommended).
- Basic understanding of HTTP and RESTful principles.
- Familiarity with Git for version control and deployment.

## Project Constraints
- The web server must handle requests concurrently, showcasing Go's efficiency in dealing with parallel processes.
- Input validation is required to ensure the server responds only to valid text or pattern requests.
- The application should provide clear error messages for unsupported or invalid inputs.

## Implementation Steps

### 1. Environment Setup
- Verify Go installation:
    ```bash
    go version
    ```
    Ensure you have Go installed on your machine. You should see the Go version if it's correctly installed.

- Create your project directory:
    ```bash
    mkdir ascii-art-service
    cd ascii-art-service
    ```

### 2. Project Initialization
- Initialize a new Go module by running:
    ```bash
    go mod init ascii-art-service
    ```
    Replace `ascii-art-service` with your preferred module name. This step creates a `go.mod` file in your project directory.

### 3. Web Server Initialization
- Create a main Go file (`main.go`) in your project directory.
- Import the `net/http` package and initialize a basic HTTP server:
    ```go
    package main

    import (
        "net/http"
    )

    func main() {
        http.HandleFunc("/", handler)
        http.ListenAndServe(":8080", nil)
    }

    func handler(w http.ResponseWriter, r *http.Request) {
        // Handler logic will go here
    }
    ```
    This code snippet sets up a simple web server that listens on port 8080.

### 4. Input Handling
- In your `handler` function, add logic to read query parameters or form values for text input:
    ```go
    text := r.URL.Query().Get("text")
    if text == "" {
        http.Error(w, "Missing text parameter", http.StatusBadRequest)
        return
    }
    ```
    This snippet extracts the `text` parameter from the request and sends an error if it's missing.

### 5. ASCII Art Generation
- Research and choose an ASCII art generation library or algorithm. For simplicity, consider using a library like `go-figure`:
    ```bash
    go get github.com/common-nighthawk/go-figure
    ```
- Incorporate the ASCII art generation in your handler:
    ```go
    import (
        "github.com/common-nighthawk/go-figure"
    )

    func handler(w http.ResponseWriter, r *http.Request) {
        text := r.URL.Query().Get("text")
        if text == "" {
            http.Error(w, "Missing text parameter", http.StatusBadRequest)
            return
        }

        asciiArt := figure.NewFigure(text, "", true).String()
        w.Write([]byte(asciiArt))
    }
    ```
    This updated handler generates ASCII art from the user-provided `text` and returns it in the response.

### 6. Testing Locally
- Run your server:
    ```bash
    go run main.go
    ```
- Test the server by visiting `http://localhost:8080/?text=YourText` in your web browser, replacing `YourText` with actual text.

### 7. Deployment
- Prepare your application for deployment. If using Heroku, create a `Procfile` in the root of your project with the following content:
    ```
    web: ascii-art-service
    ```
- Deploy your application to your chosen cloud platform. Follow the platform's specific deployment steps for Go applications.

### 8. Verification
- Once deployed, verify the live application by accessing your cloud application's URL with the appropriate query parameters, similar to local testing.


## Sample Output
For input "Go", the expected output could be:

 |
| | _
| || |
__|


## Learning Resources
- **Go Syntax & Web Servers**: [A Tour of Go](https://tour.golang.org/welcome/1) - Start here to get comfortable with Go's syntax.
- **HTTP Server Tutorial**: [Go Web Development](https://www.youtube.com/watch?v=2v11Ym6Ct9Q) - This video walks you through setting up a basic web server in Go. *(Relevant to Step 2)*
- **ASCII Art Library**: Explore libraries like [go-figure](https://github.com/common-nighthawk/go-figure) for ASCII art generation. *(Relevant to Step 4)*
- **Deployment Guide**: [Deploying Go Apps on Heroku](https://devcenter.heroku.com/articles/deploying-go) provides a comprehensive guide to deploying Go applications on Heroku. *(Relevant to Step 7)*

Remember, the key to this project is exploring and understanding each step. Take your time, experiment with different approaches, and enjoy the learning process!

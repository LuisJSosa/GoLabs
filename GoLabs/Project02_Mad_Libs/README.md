# Mad Libs Project

## Table of Contents
1. [Overview](#overview)
2. [Fields Focus](#fields-focus)
3. [Key Concept Coverage](#key-concept-coverage)
4. [Project Requirements](#project-requirements)
5. [Project Constraints](#project-constraints)
6. [Implementation Steps](#implementation-steps)
7. [Sample Interaction](#sample-interaction)
8. [Learning Resources](#learning-resources)

## Overview
This project involves creating a web-based Mad Libs game where users fill in blanks to complete stories. It's designed to deepen understanding of user input handling, string manipulation, and dynamic content generation in Go, along with an introduction to web development and platform engineering.

## Fields Focus
- **Backend Development**: Developing the logic to dynamically insert user-provided words into story templates.
- **Platform Engineering**: Deploying the application to allow user interaction through a web interface.

## Key Concept Coverage
- **Variables and Types**: Utilizing different data types to store user inputs and template components.
- **String manipulation**: Implementing string operations to merge user inputs into story templates.

## Project Requirements
- Go environment setup for development.
- Basic knowledge of HTML for creating web forms.
- Understanding of handling HTTP requests in Go.

## Project Constraints
- Ensure the web application is responsive and user-friendly.
- Validations for user inputs to prevent empty submissions.
- Clear instructions for users on what types of words are expected (noun, verb, adjective, etc.).

## Implementation Steps

### 1. Environment and Project Setup
- Confirm Go is installed by running `go version` in your terminal.
- Create a new directory for your Mad Libs project and navigate into it.

### 2. Initialize Go Module
- Initialize a Go module to manage dependencies:
    ```bash
    go mod init mad-libs
    ```

### 3. Create Web Form
- Develop an HTML form to collect words from users. Each input field should correspond to a part of speech needed for the Mad Libs story.

### 4. Web Server Setup
- In your Go application, import `net/http` and set up a basic web server:
    ```go
    package main

    import (
        "net/http"
        "html/template"
    )

    func main() {
        http.HandleFunc("/", formHandler)
        http.ListenAndServe(":8080", nil)
    }
    ```
- Implement `formHandler` to render the HTML form and handle form submissions.

### 5. Handling Form Submission
- Parse the form data submitted by the user:
    ```go
    func formHandler(w http.ResponseWriter, r *http.Request) {
        if r.Method == "POST" {
            // Process form values
        }
        // Render the form template
    }
    ```

### 6. Generating the Mad Libs Story
- After form submission, use the provided words to fill in the blanks of your Mad Libs template and generate the story.
- Display the completed story to the user.

### 7. Local Testing
- Test the application locally by running `go run .` and visiting `http://localhost:8080` in your browser.

### 8. Deployment
- Prepare your application for deployment, possibly using Docker for consistency.
- Choose a platform (e.g., Heroku, AWS) and follow their guide to deploy your Go web application.

## Sample Interaction
User is prompted with a web form asking for various words (noun, verb, adjective). Upon submission, the user sees a humorous story incorporating their words, like:

"Today, I went to the zoo. I saw a(n) **gigantic** **elephant** **jumping** up and down in its tree."

## Learning Resources
- **HTML Forms**: [HTML Form Basics](https://developer.mozilla.org/en-US/docs/Learn/Forms/Your_first_form) for creating user input forms.
- **Go Web Development**: [Building Web Applications with Go](https://www.youtube.com/watch?v=Vlie-srOU8c) for understanding web server setup and request handling in Go.
- **Deploying Go Applications**: [Deploy Go apps on Heroku](https://devcenter.heroku.com/articles/deploying-go) for guidelines on deploying Go applications to Heroku.

Remember to test each part of your application thoroughly and enjoy the creative process of making learning fun through Mad Libs!

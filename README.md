# first-serverless-container
## Installation

To install Docker, follow these steps:

1. Download Docker from the [official Docker website](https://www.docker.com/get-started).
2. Follow the installation instructions for your operating system.
3. Verify the installation by running the following command in your terminal:

```sh
docker --version
```

You should see the Docker version information if the installation was successful.

## Creating a GitHub Account

To create a GitHub account, follow these steps:

1. Go to the [GitHub signup page](https://github.com/join).
2. Fill in the required information (username, email, and password).
3. Complete the verification process.
4. Click on the "Create account" button.
5. Follow the instructions to set up your profile.

You now have a GitHub account!

## Installing Go (Golang)

To install Go, follow these steps:

1. Download Go from the [official Go website](https://golang.org/dl/).
2. Follow the installation instructions for your operating system.
3. Verify the installation by running the following command in your terminal:

```sh
go version
```

You should see the Go version information if the installation was successful.

## Creating a Simple Go Application

To create a simple Go application, follow these steps:

1. Create a new file named `main.go` in your project directory.
2. Open the `main.go` file in a text editor and add the following content:

```go
package main

import (
    "fmt"
    "net/http"
)

func helloHandler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, World!")
}

func main() {
    http.HandleFunc("/", helloHandler)
    fmt.Println("Server is running on port 8080")
    http.ListenAndServe(":8080", nil)
}
    ```

3. Save the `main.go` file.
4. Initialize a new Go module in your project directory by running the following command in your terminal:

```sh
go mod init your-module-name
```

5. Download the necessary dependencies by running:

```sh
go mod tidy
```

This Go application sets up a basic web server that responds with "Hello, World!" when accessed.


## Building a Dockerfile

To start building a Dockerfile, follow these steps:

1. Create a new file named `Dockerfile` in the root of your project directory.
2. Open the `Dockerfile` in a text editor and define the base image. For example, to use the official Golang image, add the following line:

```Dockerfile
FROM golang:1.17-alpine
```

3. Set the working directory inside the container:

```Dockerfile
WORKDIR /app
```

4. Copy the current directory contents into the container:

```Dockerfile
COPY . .
```

5. Install any needed dependencies:

```Dockerfile
RUN go mod tidy
```

6. Build the Go app:

```Dockerfile
RUN go build -o main .
```

7. Make port 8080 available to the world outside this container:

```Dockerfile
EXPOSE 8080
```

8. Define the command to run the executable:

```Dockerfile
CMD ["./main"]
```

Your `Dockerfile` should look like this:

```Dockerfile
FROM golang:1.17-alpine
WORKDIR /app
COPY . .
RUN go mod tidy
RUN go build -o main .
EXPOSE 8080
CMD ["./main"]
```

9. Save the `Dockerfile` and build the Docker image by running the following command in your terminal:

```sh
docker build -t your-image-name .
```

10. Run the Docker container:

```sh
docker run -p 8080:8080 your-image-name
```

11. Open a web browser and navigate to http://localhost:8080

Your application should now be running inside a Docker container!
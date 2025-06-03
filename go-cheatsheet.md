---
id: 12
date: 2025-06-03T00:00:00Z
title: Go Cheatsheet
author: Jeremy Novak
summary: Cheatsheet for the Go programming language
slug: go-cheatsheet
tags:
  - go
published: true
---

# Go (Golang) Cheatsheet

---

## Setup & Environment

- Install Go (macOS)
```bash
brew install go
```

- Install Go (Linux)
```bash
# Download latest Go (replace version as needed)
wget https://go.dev/dl/go1.22.2.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.22.2.linux-amd64.tar.gz
# Add to PATH (add to ~/.bashrc or ~/.zshrc)
export PATH=$PATH:/usr/local/go/bin
```

- Install Go (Windows)
1. Download the MSI installer from [https://go.dev/dl/](https://go.dev/dl/)
2. Run the installer and follow the prompts
3. Add Go to your PATH if not set automatically (usually `C:\Go\bin`)

- Check Go version
```bash
go version
```

- Set up Go environment variables (add to ~/.bashrc or ~/.zshrc)
```bash
export GOPATH="$HOME/go"
export PATH="$PATH:$GOPATH/bin"
```

- Create a new Go module/project
```bash
mkdir myproject && cd myproject
go mod init github.com/username/myproject
```

---

## Building & Running

- Run a Go file
```bash
go run main.go
```

- Build a binary
```bash
go build -o myapp main.go
```

- Install binary to $GOPATH/bin
```bash
go install
```

- Clean build cache
```bash
go clean
```

---

## Modules & Dependencies

- Add a dependency
```bash
go get github.com/sirupsen/logrus@latest
```

- List dependencies
```bash
go list -m all
```

- Tidy up go.mod and go.sum
```bash
go mod tidy
```

- Vendor dependencies
```bash
go mod vendor
```

---

## Testing

- Run all tests
```bash
go test ./...
```

- Run tests with verbose output
```bash
go test -v ./...
```

- Run tests and show code coverage
```bash
go test -cover ./...
```

- Benchmark tests
```bash
go test -bench .
```

---

## Formatting & Linting

- Format code
```bash
go fmt ./...
```

- Vet code (find suspicious constructs)
```bash
go vet ./...
```

- Lint code (requires golangci-lint)
```bash
golangci-lint run
```

---

## Common Go Commands

- Download all dependencies
```bash
go mod download
```

- List available Go tools
```bash
go tool
```

- Show documentation for a package
```bash
go doc fmt
```

- Run a Go REPL (requires gore)
```bash
gore
```

---

## Go File Structure

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

---

## Common Code Patterns

- Declare a variable
```go
var x int = 10
x := 10 // short form
```

- Declare a constant
```go
const Pi = 3.14
```

- Define a function
```go
func add(a int, b int) int {
    return a + b
}
```

- Define a struct
```go
type User struct {
    Name string
    Age  int
}
```

- Create and use a map
```go
m := make(map[string]int)
m["foo"] = 42
```

- Create and use a slice
```go
s := []int{1, 2, 3}
s = append(s, 4)
```

- For loop
```go
for i := 0; i < 10; i++ {
    fmt.Println(i)
}
```

- If/else
```go
if x > 0 {
    fmt.Println("positive")
} else {
    fmt.Println("non-positive")
}
```

- Switch
```go
switch day := 3; day {
case 1:
    fmt.Println("Monday")
case 2:
    fmt.Println("Tuesday")
default:
    fmt.Println("Other day")
}
```

- Error handling
```go
val, err := strconv.Atoi("123")
if err != nil {
    log.Fatal(err)
}
```

- Goroutine (concurrency)
```go
go func() {
    fmt.Println("Hello from goroutine")
}()
```

- Channel
```go
ch := make(chan int)
go func() { ch <- 42 }()
val := <-ch
```

---

## Working with JSON, Files, and Type Conversion

### Encoding and Decoding JSON

- Encode struct to JSON
```go
import (
    "encoding/json"
    "fmt"
)

type User struct {
    Name string `json:"name"`
    Age  int    `json:"age"`
}

user := User{Name: "Alice", Age: 30}
data, err := json.Marshal(user)
if err != nil {
    fmt.Println("error:", err)
}
fmt.Println(string(data)) // {"name":"Alice","age":30}
```

- Decode JSON to struct
```go
var user User
jsonStr := `{"name":"Bob","age":25}`
err := json.Unmarshal([]byte(jsonStr), &user)
if err != nil {
    fmt.Println("error:", err)
}
fmt.Printf("%+v\n", user) // {Name:Bob Age:25}
```

### Opening, Reading, and Closing Files

- Read entire file into string
```go
import (
    "io/ioutil"
    "fmt"
)

content, err := ioutil.ReadFile("file.txt")
if err != nil {
    fmt.Println("error:", err)
}
fmt.Println(string(content))
```

- Open file, read line by line, and close
```go
import (
    "bufio"
    "fmt"
    "os"
)

file, err := os.Open("file.txt")
if err != nil {
    fmt.Println("error:", err)
    return
}
defer file.Close()

scanner := bufio.NewScanner(file)
for scanner.Scan() {
    fmt.Println(scanner.Text())
}
if err := scanner.Err(); err != nil {
    fmt.Println("error:", err)
}
```

### String and Integer Conversion

- String to int
```go
import (
    "strconv"
    "fmt"
)

s := "123"
i, err := strconv.Atoi(s)
if err != nil {
    fmt.Println("error:", err)
}
fmt.Println(i) // 123
```

- Int to string
```go
n := 456
s := strconv.Itoa(n)
fmt.Println(s) // "456"
```

---

## Useful Packages

- "fmt" — formatted I/O
- "os" — OS functions
- "io/ioutil" — file I/O
- "net/http" — HTTP client/server
- "encoding/json" — JSON encoding/decoding
- "time" — time and date
- "log" — logging
- "context" — context for cancellation/timeouts

---

## Go Modules Example (go.mod)

```
module github.com/username/myproject

go 1.22

require (
    github.com/sirupsen/logrus v1.9.0
)
```

---

## Resources

- [Go by Example](https://gobyexample.com/)
- [Official Go Documentation](https://golang.org/doc/)
- [Go Modules Reference](https://blog.golang.org/using-go-modules)
- [Effective Go](https://golang.org/doc/effective_go.html) 
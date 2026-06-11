Setting up your Go environment correctly is the first step to becoming a productive Go developer. Here is a breakdown of how to install Go, configure your environment, and use the essential CLI tools.

---

### 1. Installation

1. **Download:** Head to the official [go.dev](https://go.dev/dl/) website and download the installer for your operating system (Windows, macOS, or Linux).
2. **Run Installer:** Follow the prompts. By default, it installs Go to `/usr/local/go` on Linux/macOS and `C:\Go` on Windows.
3. **Verify:** Open your terminal or command prompt and run:
```bash
go version

```


If it returns the installed version, Go is successfully on your system.

---

### 2. Understanding GOPATH vs. GOROOT

When you start with Go, you will hear a lot about these two environment variables. It helps to understand exactly what they do:

* **`GOROOT`**: This points to **where the Go computing language itself is installed** on your machine. You almost *never* need to change or manually set this variable anymore, as the installer handles it.
* **`GOPATH`**: This is your **workspace directory**. By default, it is located at `~/go` on Unix systems and `%USERPROFILE%\go` on Windows. It contains three main folders:
* `/bin`: Holds compiled binaries/executables installed via `go install`.
* `/pkg`: Stores cached pre-compiled packages and dependencies.
* `/src`: Where your source code used to live (historical, before Go Modules).



> **Modern Note:** Ever since the introduction of **Go Modules**, you no longer have to keep your code inside the `GOPATH/src` directory. You can create a project anywhere on your computer, run `go mod init <module-name>`, and start coding.

---

### 3. Essential Go Commands

Go comes with an incredibly powerful toolchain built right into the `go` command. You won't need third-party build tools or linters to get started.

Here are the four most important commands you need to know:

| Command | What it does | Example Usage |
| --- | --- | --- |
| **`go run`** | Compiles your code on the fly into memory and runs it immediately. Perfect for quick testing and local development. | `go run main.go` |
| **`go build`** | Compiles your code and outputs a static, standalone binary executable file. | `go build -o myapp main.go` |
| **`go fmt`** | Automatically formats your code according to strict official Go style guidelines. Never argue about tabs vs. spaces again! | `go fmt ./...` |
| **`go test`** | Automatically finds and executes any unit tests written in files ending with `_test.go`. | `go test ./...` |

#### A Quick Workflow Example:

If you have a simple `main.go` file:

1. Write your code.
2. Format it cleanly:
```bash
go fmt main.go

```


3. Run it instantly to see if it works:
```bash
go run main.go

```


4. Compile it into a production-ready file to share with others:
```bash
go build main.go

```

Now that your environment is set up, let's dive into Go's basic syntax. Go was designed at Google to be clean, readable, and minimalist.

Here is everything you need to know about variables, constants, data types, and control flow in Go.

---

### 1. Variables and Constants

Go is a **statically typed** language, meaning variable types are checked at compile-time. There are two primary ways to declare variables:

#### Standard Declaration (`var`)

Used when you want to declare a variable but might not assign a value to it immediately, or when declaring variables at the package level (outside of functions).

```go
var name string = "Alice"
var age int // Declared but not initialized. Defaults to "zero value" (0)

```

#### Short Variable Declaration (`:=`)

This is the most common way to declare and initialize variables *inside* functions. Go automatically infers the data type for you.

```go
country := "Canada" // Go infers this is a string
score := 95        // Go infers this is an int

```

#### Constants (`const`)

Constants hold values that cannot change once assigned. They must be known at compile-time.

```go
const Pi = 3.14159
const StatusOK = 200

```

---

### 2. Basic Data Types

Go keeps its primitive types straightforward. The most commonly used ones are:

| Type | Description | Examples |
| --- | --- | --- |
| `string` | Textual data | `"Hello, Go!"` |
| `int`, `int64` | Integers (whole numbers) | `42`, `-10` |
| `float64` | Floating-point (decimal) numbers | `3.14`, `0.005` |
| `bool` | Boolean logic | `true`, `false` |

> **The "Zero Value":** If you declare a variable without explicitly giving it a value, Go automatically assigns it a safe default "zero value". For `int` it's `0`, for `float64` it's `0.0`, for `string` it's `""` (empty string), and for `bool` it's `false`.

---

### 3. Control Flow

#### If / Else

In Go, you do not put parentheses `()` around your conditions, but curly braces `{}` are **mandatory**.

```go
age := 18

if age >= 21 {
    fmt.Println("Adult")
} else if age >= 13 {
    fmt.Println("Teenager")
} else {
    fmt.Println("Child")
}

```

*Bonus Feature:* Go allows an initialization statement before the condition, which limits the scope of that variable to the `if` block:

```go
if length := len(name); length > 5 {
    fmt.Println("That's a long name!")
}
// 'length' cannot be used out here

```

#### Switch Statements

Go's `switch` is a cleaner way to write multiple `if/else` conditions. Crucially, Go has an automatic `break` built-in, so code doesn't accidentally fall through to the next case.

```go
finger := 3

switch finger {
case 1:
    fmt.Println("Thumb")
case 2:
    fmt.Println("Index")
case 3:
    fmt.Println("Middle") // Code stops executing here!
default:
    fmt.Println("Other finger")
}

```

#### The `for` Loop (Go's Only Loop)

Go keeps the language minimal by only providing **one** looping keyword: `for`. However, you can use it in three different ways to mimic standard loops from other languages:

**1. The Standard 3-Component Loop (like C or Java):**

```go
for i := 0; i < 5; i++ {
    fmt.Println(i)
}

```

**2. The "While" Loop Style:**
If you omit the initialization and post statements, it acts exactly like a `while` loop.

```go
count := 1
for count <= 3 {
    fmt.Println(count)
    count++
}

```

**3. The Infinite Loop:**
Omitting the condition entirely creates a loop that runs forever until you explicitly `break` or `return`.

```go
for {
    fmt.Println("Running...")
    break // stops the infinite loop
}

```

**4. Looping over Collections (`range`):**
To iterate over arrays, slices, strings, or maps, Go uses the `range` keyword, which returns both the **index** and the **value**.

```go
fruits := []string{"apple", "banana"}

for index, value := range fruits {
    fmt.Printf("Index: %d, Value: %s\n", index, value)
}

```

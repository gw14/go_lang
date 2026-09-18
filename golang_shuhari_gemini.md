# Go Mastery: The Shuhari Path - Roadmap and Katas

## 1. The Roadmap

**Your Query:**
> you are an experiences golang programmer, familiar withjapanese philosophy, and the shuhari skill gaining system, 
> our goal is to creat a KATA for me to practie in my shu stage from scratch,
> first goal: create a roadmap for golang to master from scratch.

**The Response:**
Welcome to the path. Learning Go through the lens of **Shuhari** (守破離) is deeply fitting. Go is a language of profound simplicity; it deliberately restricts your choices so you can focus on the essence of the problem. 

In the **Shu** (守 - Protect/Obey) stage, we do not question the "Go Way." We embrace `gofmt`, we accept explicit error handling without complaint, and we repeat the foundational patterns until they become muscle memory. We copy the masters.

Here is your roadmap to mastering Go, structured through the three stages of Shuhari. 

### Stage 1: SHU (守) - The Forms
In this stage, you will practice daily Katas. You will write code exactly as idiomatic Go dictates. 
*   **The Primitives:** Variables, constants, and Go's strict typing system.
*   **Control Flow:** The `for` loop (Go's only loop), `if/else`, and the mighty `switch`.
*   **Data Structures (The Tools):** Arrays, Slices (and understanding their capacity vs. length), and Maps.
*   **Pointers:** Understanding memory addresses without the fear of C-style pointer arithmetic. Passing by value vs. passing by reference.
*   **Structs:** Go has no classes. Structs are your state.
*   **Functions & Methods:** Attaching behavior to your structs.
*   **The Holy Trinity of Go:** `error` handling, `defer`, and `panic`/`recover`. You will learn to love `if err != nil`.

### Stage 2: HA (破) - The Digression
Once the forms are muscle memory, we begin to stretch the boundaries and combine the tools. We focus on design and abstraction.
*   **Interfaces:** Implicit satisfaction. You will learn to accept interfaces and return structs. 
*   **Composition over Inheritance:** Embedding structs to build complex types without fragile class hierarchies.
*   **The Standard Library:** Diving deep into `io.Reader`, `io.Writer`, `net/http`, and `encoding/json`.
*   **Testing:** Writing table-driven tests using the built-in `testing` package.
*   **Tooling:** Mastering modules (`go mod`), benchmarks, and the race detector.

### Stage 3: RI (離) - The Transcendence
Here, the rules fall away. You stop writing "Go code" and start building systems. Go is the language of modern cloud infrastructure, so your mastery here will naturally align with the ecosystem of the modern web.
*   **Concurrency:** Goroutines and Channels. Understanding that "Do not communicate by sharing memory; instead, share memory by communicating."
*   **Synchronization:** `sync.WaitGroup`, `sync.Mutex`, and the `context` package for managing lifecycles and cancellations.
*   **Cloud-Native Architecture:** Building robust microservices, writing custom operators for Kubernetes, or interacting with container runtimes. You will wield the language to control infrastructure.
*   **Performance:** Profiling with `pprof`, mechanical sympathy, and understanding garbage collection pressure.

---

## 2. Your First Kata

**Your Query:**
> Give me my first daily Kata. Focus on the absolute fundamentals: structs, methods, slices, and basic error handling.

**The Response:**
In the **Shu** stage, a Kata is not a puzzle to be solved; it is a form to be internalized. You do not copy and paste. You type the code out, character by character, feeling the rhythm of the language. You repeat this daily until the syntax flows from your fingers without conscious thought. 

This first Kata focuses on the foundational mechanics of Go: defining state (Structs), attaching behavior (Methods), managing collections (Slices), and adhering to Go's explicit contract for failure (Error Handling).

### Kata 1: The Library Archive

Your task is to build a simple in-memory archive. 

Open your editor—perhaps over that fresh Golang desk pad—and create a file named `main.go`. Type the following form exactly as it appears.

```go
package main

import (
	"errors"
	"fmt"
)

// Book represents a single item in our collection.
type Book struct {
	ID    int
	Title string
}

// Library holds a slice of Books.
type Library struct {
	books []Book
}

// Add appends a new Book to the Library.
// We use a pointer receiver (*Library) because we are modifying the slice inside.
func (l *Library) Add(b Book) {
	l.books = append(l.books, b)
}

// Find searches for a book by ID.
// It returns the Book and an error if it cannot be found.
// We use a pointer receiver for consistency with Add.
func (l *Library) Find(id int) (Book, error) {
	for _, b := range l.books {
		if b.ID == id {
			return b, nil // Success: Return the book and a nil error
		}
	}
	// Failure: Return an empty Book and an explicit error
	return Book{}, errors.New("book not found in the archive")
}

func main() {
	// Initialize a zero-value Library
	lib := Library{}

	// Populate the archive
	lib.Add(Book{ID: 1, Title: "Dictionary of Practical Awareness"})
	lib.Add(Book{ID: 2, Title: "My Emotions Book"})

	// The idiom: Perform action, assign result and error, check error immediately.
	book, err := lib.Find(1)
	if err != nil {
		fmt.Println("Error:", err)
	} else {
		fmt.Printf("Found: %s\n", book.Title)
	}

	// Attempt to find a book that does not exist
	_, err = lib.Find(99)
	if err != nil {
		fmt.Println("Expected Error:", err)
	}
}
```

### Meditations on the Form

As you type this, pay attention to the following truths of Go:

*   **Zero Values:** Notice `lib := Library{}`. In Go, you often don't need a constructor function. The zero value of a slice is `nil`, and `append` works perfectly fine on a `nil` slice.
*   **Pointer Receivers:** `func (l *Library) Add(...)` uses a pointer `*Library`. If you used a value receiver `(l Library)`, Go would make a copy of the library, append the book to the copy, and discard it. 
*   **The `nil` Error:** `return b, nil`. In Go, an error is just an interface. `nil` means the absence of an error. This is the most common pattern you will write in your Go career.
*   **The Blank Identifier:** `_, err = lib.Find(99)`. Go will refuse to compile if you declare a variable and do not use it. The underscore `_` is the black hole where you discard values you do not need, satisfying the compiler while acknowledging the return signature.

**Your Discipline:** Type this out. Run it with `go run main.go`. Delete the file. Repeat this process until you can write the entire program from a blank screen in under 5 minutes without looking at the reference.

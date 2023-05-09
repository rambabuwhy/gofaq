# faq-2

6. What are some key features of Go's type system? How does it differ from other programming languages?

Go's type system is statically typed and strongly typed, which means that types are checked at compile time and type mismatches are not allowed. Go also has support for type inference, which allows the compiler to automatically determine the type of a variable based on its context.

Some key features of Go's type system include:

* Its support for interfaces, which are used to define sets of methods that can be implemented by different types
* Its support for structs, which are used to define custom composite types that can contain fields of different types
* Its support for type embedding, which allows one type to inherit methods and fields from another type
* Its support for method receivers, which allow methods to be associated with types and called on instances of those types

Go's type system differs from other programming languages in several ways, including its focus on simplicity and its use of interfaces for polymorphism.

Example code snippet:

```go
package main

import "fmt"

type Shape interface {
    Area() float64
}

type Rectangle struct {
    width  float64
    height float64
}

func (r Rectangle) Area() float64 {
    return r.width * r.height
}

type Circle struct {
    radius float64
}

func (c Circle) Area() float64 {
    return 3.14 * c.radius * c.radius
}

func PrintArea(s Shape) {
    fmt.Println("Area:", s.Area())
}

func main() {
    r := Rectangle{5.0, 10.0}
    c := Circle{5.0}

    PrintArea(r)
    PrintArea(c)
}
```

7. What are Goroutines and how do they differ from threads?

Goroutines are lightweight threads of execution in Go that are managed by the Go runtime. Goroutines are more efficient than threads because they have a smaller memory footprint and can be created and destroyed more quickly. Goroutines are also designed to communicate with each other using channels, which provide a way for Goroutines to safely share data without the need for locks or other synchronization primitives.

In contrast, threads are managed by the operating system and have a larger memory footprint than Goroutines. Threads also require locks or other synchronization primitives to safely share data between threads.

Example code snippet:

```go
package main

import (
    "fmt"
    "time"
)

func worker(id int, jobs <-chan int, results chan<- int) {
    for j := range jobs {
        fmt.Println("worker", id, "processing job", j)
        time.Sleep(time.Second)
        results <- j * 2
    }
}

func main() {
    jobs := make(chan int, 100)
    results := make(chan int, 100)

    for w := 1; w <= 3; w++ {
        go worker(w, jobs, results)
    }

    for j := 1; j <= 5; j++ {
        jobs <- j
    }
    close(jobs)

    for a := 1; a <= 5; a++ {
        <-results
    }
}
```

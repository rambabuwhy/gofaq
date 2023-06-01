# Basics of Go Language

1. What are the key features of Go? How does it differ from other programming languages?

Go is a statically typed, compiled programming language that is designed to be efficient, expressive, and safe. Some of the key features of Go include:

* Simple syntax and minimalist design
* Built-in support for concurrency and parallelism
* Garbage collection and memory safety
* Strong typing and type inference
* Efficient compilation and execution
* Cross-platform support

Go differs from other programming languages in several ways, including its focus on simplicity, its built-in concurrency features, and its use of interfaces for polymorphism.

Example code snippet:

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, world!")
}
```

2. How does Go support functional programming? What are some key features of Go that make it suitable for functional programming?

Go supports functional programming through its support for higher-order functions, closures, and first-class functions. Go also has some built-in functions, such as map, reduce, and filter, that are commonly used in functional programming.

Some key features of Go that make it suitable for functional programming include:

* Its support for closures and first-class functions, which allow functions to be passed as arguments and returned as results from other functions
* Its support for immutable data structures, such as arrays and maps
* Its built-in support for anonymous functions, which can be used to create function literals
* Its support for interfaces, which can be used to create generic functions

Example code snippet:

```go
package main

import "fmt"

type Mapper func(int) int

func mapInts(a []int, f Mapper) []int {
    b := make([]int, len(a))
    for i, v := range a {
        b[i] = f(v)
    }
    return b
}

func main() {
    a := []int{1, 2, 3, 4, 5}

    b := mapInts(a, func(x int) int {
        return x * 2
    })

    fmt.Println(b)
}
```

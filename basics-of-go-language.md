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

3. What are the benefits and limitations of using interfaces in Go? Provide an example of how you might use an interface in your code.

Interfaces in Go provide a way to define sets of methods that a type must implement. They promote loose coupling, abstraction, and code reuse. Benefits of using interfaces include:

* Enabling polymorphism, allowing different types to be used interchangeably based on shared behavior
* Promoting modular and testable code by defining clear contract boundaries
* Facilitating the creation of mock objects for testing purposes
* Supporting code reuse through composition and interface embedding

Limitations of interfaces in Go include:

* The inability to define instance variables or state within an interface
* The need for explicit implementation of interface methods by types
* Potential performance overhead when using interfaces due to dynamic dispatch

Example code snippet:

```go
package main

import "fmt"

type Animal interface {
	Sound() string
}

type Dog struct{}

func (d Dog) Sound() string {
	return "Woof"
}

type Cat struct{}

func (c Cat) Sound() string {
	return "Meow"
}

func main() {
	animals := []Animal{Dog{}, Cat{}}

	for _, animal := range animals {
		fmt.Println(animal.Sound())
	}
}
```

In this example, we define an `Animal` interface with a `Sound` method. The `Dog` and `Cat` types implement the `Sound` method, satisfying the `Animal` interface. By using the `Animal` interface, we can create a slice of `Animal` and iterate over it, calling the `Sound` method on each element regardless of its specific type. This demonstrates polymorphism and code reuse through interfaces.

4. What are some key features of Go's type system? How does it differ from other programming languages?

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

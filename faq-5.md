# faq-5

11. What is a pointer in Go? How are pointers used in Go?

* A pointer is a variable that stores the memory address of another value. Pointers are used to indirectly access and modify values in memory.

Example Go code snippet:

```go
var x int = 42
var p *int = &x   // p is a pointer to x
*p = 10           // Assigns 10 to the value stored at the memory address pointed by p
fmt.Println(x)    // Output: 10
```

12. What is a struct in Go? How are structs used in Go? Can you provide an example of how you might use a struct in your code?

* A struct is a composite data type that allows you to group together related values of different types into a single entity. Structs are used to create custom data structures in Go.

Example Go code snippet:

```go
type Person struct {
    Name string
    Age  int
}

func main() {
    p := Person{Name: "John", Age: 30}
    fmt.Println(p.Name, p.Age)   // Output: John 30
}
```

13. What is the difference between a slice and an array in Go? How are they used differently in Go?

* An array has a fixed length defined at compile-time and is of a specific type, whereas a slice is a dynamically-sized and flexible view into an underlying array. Slices are used more commonly as they provide more flexibility and convenience compared to arrays.

Example Go code snippet:

```go
// Array
var arr [3]int = [3]int{1, 2, 3}

// Slice
var slice []int = []int{1, 2, 3}
```

14. What is the difference between a map and a struct in Go? How are maps used in Go?

* A struct is a composite data type used to group related values together, while a map is a built-in type in Go that represents a collection of key-value pairs. Maps are used for efficient lookup and retrieval of values based on keys.

Example Go code snippet:

```go
// Struct
type Person struct {
    Name string
    Age  int
}

// Map
var m map[string]Person = make(map[string]Person)
m["John"] = Person{Name: "John", Age: 30}
```

15. How does Go support functional programming? Can you provide an example of how you might use functional programming techniques in your code?

* Go supports functional programming by providing support for higher-order functions, closures, and first-class functions. Functional programming techniques can be used to achieve code reusability and cleaner code organization.

Example Go code snippet:

```go
func multiplyBy(factor int) func(int) int {
    return func(x int) int {
        return x * factor
    }
}

func main() {
    doubler := multiplyBy(2)
    result := doubler(5)   // Output: 10
    fmt.Println(result)
}
```

These are the answers and code snippets for the first five questions. Let me know if you would like the remaining answers and code snippets.

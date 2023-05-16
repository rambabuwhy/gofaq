# faq-7

21. How does Go support error handling? What are some best practices for handling errors in Go?

* Go uses multiple return values, including the common practice of returning an error as the last value. Best practices for error handling in Go include checking and handling errors explicitly, avoiding excessive error wrapping, and utilizing error types for specific cases.

Example Go code snippet:

```go
func divide(x, y float64) (float64, error) {
    if y == 0 {
        return 0, errors.New("division by zero")
    }
    return x / y, nil
}

func main() {
    result, err := divide(10, 0)
    if err != nil {
        fmt.Println("Error:", err)
        return
    }
    fmt.Println("Result:", result)
}
```

22. What is a defer statement in Go? How is it used? Can you provide an example of how you might use a defer statement in your code?

* A defer statement is used to schedule a function call to be executed just before the surrounding function returns. It is often used to ensure that resources are properly released or clean-up operations are performed.

Example Go code snippet:

```go
func main() {
    fmt.Println("Start")
    defer fmt.Println("Middle")
    fmt.Println("End")
}
// Output:
// Start
// End
// Middle
```

23. How does Go handle type assertions and type switches? Can you provide an example of how you might use type assertions or type switches in your code?

* Type assertions and type switches are used to inspect and work with values of interface type. Type assertions allow you to extract the underlying concrete type, while type switches enable conditional handling based on the underlying type.

Example Go code snippet with type assertion:

```go
var val interface{} = "Hello"
str, ok := val.(string)
if ok {
    fmt.Println("String:", str)
}
```

Example Go code snippet with type switch:

```go
func process(val interface{}) {
    switch v := val.(type) {
    case string:
        fmt.Println("String:", v)
    case int:
        fmt.Println("Int:", v)
    default:
        fmt.Println("Unknown type")
    }
}
```

24. What is a variadic function in Go? How is it used? Can you provide an example of how you might use a variadic function in your code?

* A variadic function is a function that can accept a variable number of arguments of the same type. Variadic functions are invoked by passing multiple arguments of the specified type, or by passing a slice of the specified type with the `...` ellipsis notation.

Example Go code snippet:

```go
func sum(nums ...int) int {
    total := 0
    for _, num := range nums {
        total += num
    }
    return total
}

func main() {
    result := sum(1, 2, 3, 4, 5)   // Output: 15
    fmt.Println(result)
}
```

25. What is a type in Go? How are types defined and used in Go?

* A type in Go is a description of the nature and properties of a value. Types can be basic types (e.g., int, string), composite types (e.g., struct, array), or user-defined types. Types are defined using type declarations and can be used to create variables, function signatures, or struct fields.

Example Go code snippet:

```go
type Person struct {
    Name string
    Age  int
}

func main() {
    var x int       // basic type
    var s string    // basic type
    var arr [3]int  // array type
    var p Person    // user-defined type

    fmt.Println(x)    // Output: 0
    fmt.Println(s)    // Output: ""
    fmt.Println(arr)  // Output: [0 0 0]
    fmt.Println(p)    // Output: { 0}
}
```

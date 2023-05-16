# faq-6

16. What is the purpose of a mutex in Go? How do mutexes enable synchronization between Goroutines?

* A mutex (short for mutual exclusion) is used to synchronize access to shared resources in concurrent Go programs. It allows only one Goroutine to access the shared resource at a time, ensuring that data integrity is maintained.

Example Go code snippet:

```go
import (
    "sync"
)

var counter int
var mutex sync.Mutex

func increment() {
    mutex.Lock()
    defer mutex.Unlock()
    counter++
}

func main() {
    var wg sync.WaitGroup
    for i := 0; i < 1000; i++ {
        wg.Add(1)
        go func() {
            defer wg.Done()
            increment()
        }()
    }
    wg.Wait()
    fmt.Println(counter)  // Output: 1000
}
```

17. How does Go handle garbage collection? What are some best practices for garbage collection in Go?

* Go uses a concurrent garbage collector that automatically reclaims memory that is no longer in use. Some best practices for garbage collection in Go include minimizing unnecessary allocations, avoiding circular references, and using the `sync.Pool` package for efficient reuse of objects.

18. What are the benefits and limitations of using the standard library in Go? Can you provide an example of how you might use a standard library package in your code?

* The standard library in Go provides a rich set of packages for common tasks, offering convenience, stability, and community support. Benefits include reduced development time and increased code reliability. However, the standard library may not cover every use case, requiring the use of third-party libraries for certain specialized functionalities.

Example Go code snippet:

```go
import (
    "fmt"
    "net/http"
)

func main() {
    resp, err := http.Get("https://www.example.com")
    if err != nil {
        fmt.Println("Error:", err)
        return
    }
    defer resp.Body.Close()

    // Process the HTTP response
}
```

19. What is a closure in Go? How are closures used in Go? Can you provide an example of how you might use a closure in your code?

* A closure is a function that captures and references variables from its surrounding lexical scope. Closures are useful for creating functions with persistent state or for creating functions on the fly.

Example Go code snippet:

```go
func makeAdder(x int) func(int) int {
    return func(y int) int {
        return x + y
    }
}

func main() {
    addFive := makeAdder(5)
    result := addFive(3)   // Output: 8
    fmt.Println(result)
}
```



20. What is the difference between a function and a method in Go? How are methods used in Go? Can you provide an example of how you might use a method in your code?

* In Go, a function is a standalone block of code that can be called with provided arguments, while a method is a function associated with a specific type. Methods are used to define behaviors or actions that can be performed by instances of a particular type.

Example Go code snippet:

```go
type Rectangle struct {
    width  int
    height int
}

func (r Rectangle) Area() int {
    return r.width * r.height
}

func main() {
    rect := Rectangle{width: 5, height: 10}
    fmt.Println(rect.Area()) 
    // Output: 50
}
```

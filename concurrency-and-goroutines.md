# Concurrency and Goroutines

1. How does Go handle concurrency? What are some common patterns for concurrent programming in Go?

Go has built-in support for concurrency through Goroutines and channels. Goroutines are lightweight threads that can be started with the "go" keyword, and channels allow for communication and synchronization between Goroutines.

Some common patterns for concurrent programming in Go include:

* Fan-out/fan-in: breaking up work into smaller tasks and distributing them across multiple Goroutines, then collecting the results
* Worker pool: creating a fixed number of Goroutines to handle incoming tasks from a queue
* Pipeline: chaining together a series of Goroutines to process data in stages

Example code snippet:

```go
package main

import "fmt"

func worker(id int, jobs <-chan int, results chan<- int) {
    for j := range jobs {
        fmt.Println("worker", id, "processing job", j)
        results <- j * 2
    }
}

func main() {
    jobs := make(chan int, 100)
    results := make(chan int, 100)

    for w := 1; w <= 3; w++ {
        go worker(w, jobs, results)
    }

    for j := 1; j <= 9; j++ {
        jobs <- j
    }
    close(jobs)

    for a := 1; a <= 9; a++ {
        <-results
    }
}
```

2. Explain the difference between a Goroutine and a thread. How do Goroutines achieve concurrency?

Goroutines are lightweight threads of execution in Go that are managed by the Go runtime. Goroutines are more efficient than threads because they have a smaller memory footprint and can be created and destroyed more quickly. Goroutines are also designed to communicate with each other using channels, which provide a way for Goroutines to safely share data without the need for locks or other synchronization primitives.

In contrast, threads are managed by the operating system and have a larger memory footprint than Goroutines. Threads also require locks or other synchronization primitives to safely share data between threads.

Goroutines are similar to threads in that they can execute concurrently with other Goroutines, but they are different in several ways:

* Goroutines are managed by the Go runtime and are more lightweight than threads
* Goroutines have a much smaller stack size than threads, so many more Goroutines can be created than threads
* Goroutines are multiplexed onto a smaller number of OS threads, so they can be scheduled more efficiently

Goroutines achieve concurrency through cooperative multitasking, which means that the Go scheduler decides when to switch between Goroutines based on certain conditions, such as I/O operations or function calls.

Example code snippet:

```go
package main

import (
    "fmt"
    "time"
)

func say(s string) {
    for i := 0; i < 5; i++ {
        time.Sleep(100 * time.Millisecond)
        fmt.Println(s)
    }
}

func main() {
    go say("world")
    say("hello")
}
```

# Error Handling

1. How does Go handle errors? What are some best practices for error handling in Go?

Go uses return values to indicate errors, and the convention is to return an error as the last value in a function call. Go also provides a built-in `error` type that can be used to represent errors in a consistent way.

Some best practices for error handling in Go include:

* Always check the error returned by a function call and handle it appropriately
* Use the `errors` package or create custom error types to provide descriptive error messages
* Use the `fmt.Errorf` function or the `errors.New` function to create new error instances
* Prefer returning errors as values rather than using panic and recover for exceptional situations
* Handle errors at the appropriate level of abstraction, either by returning them or handling them locally
* Use `defer` to ensure that resources are properly cleaned up, even in the presence of errors

Example code snippet:

```go
package main

import (
	"errors"
	"fmt"
	"os"
)

func readFile(filename string) ([]byte, error) {
	file, err := os.Open(filename)
	if err != nil {
		return nil, fmt.Errorf("failed to open file: %w", err)
	}
	defer file.Close()

	data := make([]byte, 1024)
	_, err = file.Read(data)
	if err != nil {
		return nil, fmt.Errorf("failed to read file: %w", err)
	}

	return data, nil
}

func main() {
	data, err := readFile("example.txt")
	if err != nil {
		fmt.Println("Error:", err)
		return
	}

	fmt.Println("File content:", string(data))
}
```

In the above example, the `readFile` function reads the content of a file. If any error occurs while opening or reading the file, it returns an error value with an informative message using `fmt.Errorf`. The main function then checks the error returned by `readFile` and handles it accordingly.

2. How does Go handle errors in Goroutines? What are some best practices for error handling in concurrent Go programs?

In Go, errors in Goroutines can be handled using a combination of error return values and channels for error communication. It's important to propagate errors from Goroutines to the calling code to ensure proper error handling.

Some best practices for error handling in concurrent Go programs include:

* Use separate channels to communicate results and errors from Goroutines.
* Use a `sync.WaitGroup` or other synchronization mechanisms to wait for Goroutines to finish and collect their results and errors.
* Consider using a `select` statement to handle multiple Goroutines concurrently and handle errors as they occur.
* Wrap Goroutine calls in a higher-level function that can handle errors and provide proper context.
* Use a dedicated Goroutine to handle errors from other Goroutines and centralize error logging or reporting.

Example code snippet:

```go
package main

import (
	"fmt"
	"sync"
)

func process(data int, result chan<- int, errChan chan<- error) {
	// Perform some computation
	if data > 100 {
		errChan <- fmt.Errorf("data value %d is too large", data)
		return
	}

	// Send the result back
	result <- data * 2
}

func main() {
	data := []int{10, 20, 30, 200, 40}

	resultChan := make(chan int)
	errChan := make(chan error)
	var wg sync.WaitGroup

	for _, d := range data {
		wg.Add(1)
		go func(d int) {
			defer wg.Done()
			process(d, resultChan, errChan)
		}(d)
	}

	go func() {
		wg.Wait()
		close(resultChan)
		close(errChan)
	}()

	for r := range resultChan {
		fmt.Println("Result:", r)
	}

	for err := range errChan {
		fmt.Println("Error:", err)
	}
}
```

In this example, a set of integers is processed concurrently in Goroutines. The `process` function performs some computation on each integer and sends the result back through the `result` channel. If the data value is too large, an error is sent through the `errChan`. The main Goroutine waits for all Goroutines to finish using a `sync.WaitGroup` and collects the results and errors through separate channels. Finally, the results and errors are printed accordingly.

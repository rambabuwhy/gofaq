# faq-10

**32. What is the purpose of the init() function in Go? When and how is it executed?**

In Go, the `init()` function is a special function that is executed automatically before the `main()` function in a package. Its purpose is to perform any initialization tasks or setup required by the package.

Here's an example to demonstrate the usage of `init()` function:

```go
goCopy codepackage main

import "fmt"

func init() {
	fmt.Println("Initializing...")
	// Perform initialization tasks here
}

func main() {
	fmt.Println("Main function")
	// Rest of the program
}
```

In the above code, the `init()` function is defined without any parameters or return types. It gets executed automatically before the `main()` function. In this example, it simply prints "Initializing..." to the console. The `main()` function is called after the `init()` function, and it is the entry point of the program.

When we run the code, the output will be:

```bash
bashCopy codeInitializing...
Main function
```

The `init()` function is executed only once per package, regardless of the number of times the package is imported. If a package is imported multiple times in the same program, the `init()` function will run only once.

It's worth noting that the `init()` function is commonly used for setting up variables, initializing data structures, registering components, or performing any necessary setup actions before the program starts executing.

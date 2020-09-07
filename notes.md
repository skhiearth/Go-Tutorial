# Golang Tutorial

## Introduction

Go was created by a small team within Google comprising of Robert Griesemar, Rob Pike and Ken Thompson.

1. Strong (type of a variable can't be changed) and statically typed (variables need to be defined at compile time)

2. Excellent community

3. Simplicity, Fast compile times, Built-in concurrency, compiles down to standalone binaries and Garbage collection

### Resources

1. golang.org

2. golangbridge.org

3. play.golang.org

### Hello, world

```go
package main // packages

import (
    "fmt" // to format strings
)

func main() { // main function - entry point
    fmt.Println("Hello, world!") // print function from fmt library
}
```

## Setting up a Developer Enviornment

![https://golang.org/dl/](Download Go Binary)

Download GoLand from JetBrains

## Variables

```go
package main

import (
    "fmt"
)

func main() {
    var i int // keyword name type - used when we want declare variable but not use it yet
    i = 42
    var j int = 42 // keyword name type = value - useful when go doesn't have enough enough to automatically pickup type of a variable, e.g sometimes we want to use it as a float and not as an integer
    k := 2 // automatic type pickup
    fmt.Println(i)
}
```

### Variable Declaration

Outside of the scope of a function, we have to use the complete declaration prototype (`keyword name type`)

```go
package main

import (
    "fmt"
)

var i float32 = 50

func main() {
    fmt.Printf("%v, %T", i, i)
}
```

Block of variables declared together;

```go
package main

import (
    "fmt"
)

var (
    name string = "foo"
    lname string = "bar"
    numb int = 3
    season int = 11
)

func main() {
    fmt.Printf("%v, %T", i, i)
}
```

### Redeclaration and Shadowing

We can't redeclare variables, but can shadow them.

```go
package main

import (
    "fmt"
)

var i int = 27

func main() {
    var i int = 42
    i = 13 // can't use i := 13 because we can't define same variable twice within the same scope
    // Shadowing: Inner most scope takes precedence
    fmt.Println(i)
}
```

### Visiblity

Uppercase first letter (I) -> Global Scope or Export, i.e., Compiler automatically assigns it to the global scope
Lowercase first letter (i) -> Package Scope
Lowercase (i) -> Block Scope

```go
package main

import (
    "fmt"
)

func main() {
    var i int = 42
    j := 13 // compile time error because j is defined but not used
    fmt.Println(i)
}
```

### Naming conventions

PascalCase or camelCase

Capitalize acronyms (e.g., HTTP)

Tip: Length of a variable defines the life-span of a variable.

### Type conversions

destinationType(variable)

#### Integer -> Float32

```go
package main

import (
    "fmt"
)

func main() {
    var i int = 42
    var j float32
    j = float32(i) // Explicit conversion is mandatory
    fmt.Println(j)
}
```

#### Float32 -> Integer (Losing Information)

```go
package main

import (
    "fmt"
)

func main() {
    var i float32 = 42.5
    var j int
    j = int(i)
    fmt.Println(j)
}
```

#### Integer -> String

```go
package main

import (
    "fmt"
    "strconv" // String conversion package
)

func main() {
    var i int = 42
    var j string
    j = strconv.Itoa(i) // Method from package
    fmt.Println(j)
}
```

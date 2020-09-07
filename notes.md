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

[Download Go Binary](https://golang.org/dl/)

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

## Primitives

### Boolean type

```go
package main

import (
    "fmt"
)

func main() {
    var n bool = true
    fmt.Printf("%v, %T\n", n, n)
}
```

Booleans can be used for state flagging.

```go
package main

import (
    "fmt"
)

func main() {
    n := 1 == 1 // check if 1 equals 1
    fmt.Printf("%v, %T\n", n, n) // generates a boolean
}
```

In Go, everytime we init a variable, it has a zero value and the zero value for booleans is false.

```go
package main

import (
    "fmt"
)

func main() {
    var n bool
    fmt.Printf("%v, %T\n", n, n) // generates a boolean
}
```

### Numeric types: Integers, floating point and complex numbers

Zero value for all numeric type is zero, or the zero equivalent of that numeric type (e.g., 0.0)

```go
package main

import (
    "fmt"
)

func main() {
    n := 42 // Integer (8bit, 16, 32, 64)
    var m uint16 = 42 // Unsigned Integer (8bit, 16, 32)

    // Arithmetic Operations
    fmt.Println(a + b) // Addition
    fmt.Println(a - b) // Subtraction
    fmt.Println(a * b) // Multiply
    fmt.Println(a / b) // Divide
    fmt.Println(a % b) // Modulo Function -> Remainder

    var o int8 = 3
    var p int = 10
    z := 2.1e14 // 10^14
    fmt.Println(p + int(o)) // Type Conversion

    // Bit Operations
    a := 10
    b := 3
    fmt.Println(a & b) // AND
    fmt.Println(a | b) // OR
    fmt.Println(a ^ b) // XOR
    fmt.Println(a &^ b) // ANDNOT

    // Bit Shifting
    fmt.Println(a << 3) // Bitshift left three places
    fmt.Println(a >> 3) // Bitshift right three places

    // Complex Numbers
    var com complex64 = 1 + 2i
    fmt.Printf("%v, %T\n", com, com)
    real(n) // Real part
    imag(n) // Imaginary part

    var com2 complex128 = complex(5, 12) // Another way of declaring complex number
}
```

### Text Types

A string in Go is any UTF8 character. This makes them very powerful, but as a result, they can't encode every character.

```go
package main

import (
    "fmt"
)

func main() {
    s := "this is a string
    fmt.Printf("%v, %T\n", string(s[2]), s[2]) // slicing the 3rd element in the string - strings in go are actually treated as bytes

    s[2] = "u" // compile-time error

    s2 := "add"
    fmt.Printf("%v, %T\n", s+s2, s+s2) // String Concatenation

    by := []byte(s) // Corresponding UTF values of every element in the String as an array - used for functions as a lot of function in Go work with Byte slices
}
```

A rune represented UTF32 characters. Any UTF32 character can be upto 32 bits long, but it does NOT have to be that long. Normally, special methods are required to process runes.

```go
package main

import (
    "fmt"
)

func main() {
    var r rune = 'a' // Single quotes
    fmt.Printf("%v, %T\n", r, r)

    // Runes are a true-type alias of int32
}
```

## Constants

### Naming Convention

```go
package main

import (
    "fmt"
)

func main() {
    const camelCase int = 2 // Internal Constant
    const CamelCase int = 2 // External Constant
}
```

### Typed Constants

```go
package main

import (
    "fmt"
)

func main() {
    const camelCase int = 2 // Typed Constant
}
```

Constants can be shadowed, like variables.

### Untyped Constants

```go
package main

import (
    "fmt"
)

func main() {
    const a = 2 // Untyped Constant
    var b int16 = 3

    fmt.Printf("%v, %T\n", a+b, a+b) // Implicit conversions are possible with constant because the compiler converts every instance of that constant with the designated type.
}
```

### Enumerated Constants

```go
package main

import (
    "fmt"
)

const (
    a = iota
    b // infers pattern of assignment in block and makes this iota automatically
    c // infers pattern of assignment in block and makes this iota automatically
 ) // a counter used for enumerated constants

const (
    ab = iota
)
func main() {
    fmt.Printf("%v", a) // prints 0
    fmt.Printf("%v", b) // prints 1
    fmt.Printf("%v", c) // prints 2
    fmt.Printf("%v", ab) // prints  0 - iota limited to constant block
}
```

### Enumeration Expressions

Operations that can be determined at compile time are allowed: Arithmetic, Bitwise and Bitshifting


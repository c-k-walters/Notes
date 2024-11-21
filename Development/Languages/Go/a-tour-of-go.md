# A Tour of Go

## Packages
Every Go program is made up of packages.
```go
package main

import (
    "fmt"
)

func main() {
    fmt.Preintln("Hello World")
}
```
Notice the parenthesized "factored" import statements.
You can also add individual import statements. `import "fmt"`
In Go, only capatalized functions or variables, etc are exported.

## Functions
### Basics
```go
func add(x int, y int) int {
    return x + y
}
```
This could also be rewritten while omitting types of consecutive parameters of the same type.
```go
func add(x, y int) int { return x + y }
```
It is also possible to return multiple results.
```go
func swap(x, y string) (string, string) { return "", "" }
```

### Named return types
Go's return values may also be named. If so, they are treated as variables.
```go
func split(sum int) (x, y int) {
    x = sum * 4 / 9
    y = sum - x
    return
}
```

## Variables
Here are some basic variable definitons.
```go
var c, python, java bool
var i, j int = 1, 2
k := 3

const Pi = 3.14
```


### Basic Types
1. bool
2. string
3. int, int8, int16, int32, int64
4. uint, uint8, uint16, uint32, uint64, uintptr
5. byte // alias for uint8
6. rune // alias for int32
7. float32 float64
8. complex64 comlex 128

Variables without an explicit inital value are given a zero value.
The zero value is:
- 0 for numeric types,
- false for booleans
- "" for empty strings

The expression `T(v)` converts a value `v` to the type `T`.

## For


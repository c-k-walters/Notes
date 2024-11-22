# A Tour of Go

## The Basics

### Packages
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

### Functions
#### Basics
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

#### Named return types
Go's return values may also be named. If so, they are treated as variables.
```go
func split(sum int) (x, y int) {
    x = sum * 4 / 9
        y = sum - x
        return
}
```

### Variables
Here are some basic variable definitons.
```go
var c, python, java bool
var i, j int = 1, 2
k := 3

const Pi = 3.14
```


#### Basic Types
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

### For
    Go has only one looping construct, the `for` loop.
    The basic `for` loop has three components seperated by semicolons:
    1. init statement
    2. condition expression
    3. post statement: executed at end of every iteration
    ```go
    for i:= 0; i < 10; i++ { ... }
    ```

    The init and post statements are optional.
    ```go
    for ; sum < 1000; { ... }

    // or simpler still
    for sum < 1000 { ... }
    ```
    If you omit the loop condition it loops forever.
    ```go
    for { ... }
    ```

### If
    Go supports basic if statements unwrapped
    ```go
    if v < lim { ... }
    ```

    Like for loops, if statements can also have a short statement executed before the condition.
    ```go
    if v:= 100; v < lim { ... }
    ```
    Variables declared by the statement are scoped to the end of the if.

    ```go
    if v:= 100; v < lim { ... }
    else { ... }
    ```

### Switch
    ```go
    switch os := runtime.GOOS; os {
        case "darwin":
            // ...
        case "linux":
            // ...
        default:
            // ...
    }
```

Switch without a condition is treated like an if-then-else chain.
```go
switch {
    case t.Hour() < 12:
        // ...
        // ..
}
```
### Defer
A defer statement defers the execution of a function until the surrounding function
returns; however, the deferred call's arguments are evaluated immediately.

```go
func main() {
    defer fmt.Println("world")

        // ...
}
```
Deferred function calls are pushed onto a stack.
Deferred calls are executed in last-in-first-out order.

### Pointers
The type `*T` is a pointer to a `T` value.
Its zero value is nil.
```go
var p *int
```

The `&` oeprator generates a pointer to its operand.
```go
i := 42
p = &i // p is a pointer!
```

The `*` operator denotes the pointer's underlying value.
Using this operator is known as 'dereferencing` or 'indirecting`.
    ```go
fmt.Println(*p)
    *p = 21
    ```

### Structs
    A `struct` is a collection of fields
    ```go
    type Vertex struct {
        X int
            Y int
    }

var (
        v1 = Vertex{1, 2} // has type Vertex
        p = &Vertex{X: 1} // has type *Vertex, Y:0 is implicit
    )
```

### Arrays
The type [n]T is an array of `n` values of type `T`.
```go
var a [10]int
primes := [6]int{2, 3, 5, 7, 11, 13}
```
An array's length is part of its type.
So arrays cannot be resized.

### Slices
An array has a fixed size.
A slice on the other hand, is a dynamially-sized, flexible view into the 
elements of an array. 
The type `[]T` is a slice with elements of type `T`.
Slices are kinda like references to arrays.
They do not themselves store any data.

#### Slice Literal
```go
v := []bool{true, false, true}
```
This builds the underlying array and then builds a slice that references it.
<br><br>
Slice defaults allow you to omit the lower or upper bound. ie:
```go
a[0:10]
a[:10]
a[0:]
a[:]
```
A slice has both length and capacity. 
The length of a slice is the number of elements it contains.
The capacity of a slice is the number of elements in the underlying array.
The length and capacity may be accessed from `len(s)` and `cap(s)`.
<br><br>
The zero value of a slice is `nil`.
A nil slice has a length and capacity of 0 and has no underlying array.
Slices can be created with the built-in `make` function.
```go
a := make([]int, 5) // len(a)==5 ie [0, 0, 0, 0, 0]
b := make([]int, 0, 5) // len(b)==0 cap(b)==5
b := b[:cap(b)]

c := [][]string{ []string{"-", "-"}, ... }
```
You may also append to a slice. 
If the backing array is too small to fit all the given values a bigger array
will be allocated.
```go
func append s[]T, vs ...T) []T
```

### Range
The `range` form of the `for` loop iterates over a slice or map.
Two values are returned for each iteration.
The first is the index, and the second is a copy of the element at that index.
You can ignore either of these values.
```go
for i, v := range pow { ... }
for _, v := range pow2 { ... }
```

### Maps
A map maps keys to values.
The zero value of a map is nil.
A nil map has no keys, nor can keys be added.
The make function returns a map of the given type, initalized.
```go
    var m map[string]int
m = make(map[string]int)

    m = map[string]int{
        "foo": 0,
            "bar": 1,
    }

var b = map[string]Vertex{
    "Bell Labs": {40.68433, -74.39967}, // notice that we omit the type name
        "Google":    {37.42202, -122.08408},
}
```

Insert or update or retrieve or delete an element in map m:
```go
m[key] = elem
    elem = m[key]
delete(m, key)
    ```

    You may also test that a key is present with two-value assignment.
    `ok` is `true` if `key` is in `m`.
    ```go
    elem, ok := m[key]
    ```

### Function values
    Functions are values too.
    Function values may be used as function arguments and return values.
    ```go
    func compute(fn func(float64, float64) float64) float64 { ... }
    \\ same synt. as normal func definiton
    ```

    Go functions may be closures.
    A closure is a function value that references variables from outside its body.
    For example, the `adder` function returns a closure.
    Each closure is bound to its own `sum` variable.
    ```go
    func adder() func(int) int {
sum := 0
         return func(x int) int {
             sum += x
                 return sum
         }
    }
```

## Methods and Interfaces

### Methods
Go does not have classes.
However, you can define methods on types.
A method is a function with a speial *reciever* argument.
```go
type Vertex struct { X, Y float64 }

func (v Vertex) Abs() float64 { ... }

v := Vertex{}
v.Abs()
    ```

    You can declare a method on non-struct types too.
    You can only declare a method with a reciever whose type is defined in the 
    same package as the method.
    This includes built-in types like `int`
    ```go
    type MyFloat flaot64

    func (f MyFlaot) Abs() float64 { ... }
    ```

    You can declare methods with pointer receivers.
    These methods operates on the reciever itself.
    ```go
    func (v *Vertex) Scale(f float64) { ... }
    ```

### Interfaces
    An interface type is defined as a set of method signtitures.
    A value of interface type can hold any value that implememnts those methods.
    ```go
    type I interface {
        M()
    }

type T struct {
    S string
}

func (t T) M() { ... } // T implicitly implememnts I
```

Under the hood, interface values can be though of as a tuple of a value and a
concrete type: `(value, type)`
If the underlying value inside of the interface is nil, the method will be
called with a nil reciever.
This is different from a nil interface.
Callng a method on a nil interface is a run-time error.

### Empty Interface
```go
interface{}
```

An empty interface holds values of any type. 
We can perform a type assertion to access an interface's underlying value's
underlying concrete value.
```go
var i interface{} = "hello"

s, ok := i.(string) // "hello" string, true
    f, ok := i.(float64) // 0, false
f = i.(float64) // panic
    ```

### Type Switch
    ```go
    switch v := i.(type) {
        case int:
            // ...
        default:
            // ...
    }
```

### Stringers
One of the most ubiquitous interfaces is `Stringer` defined by the fmt package.
A `Stringer` is a type that can describe itself as a string.
```go
type Stringer interface {
    String() string
}
```

### Errors
The `error` type is a built-in interface. 
```go
type error interface {
    Error() string
}
```

### Readers
The `io` package specifies the io.Reader interface, which represents the read
end of a stream of data. 
Here is a sample of the interface.
    ```go
func (T) Read(b []byte) (n int, err error)
    ```

## Generics
    Go functions can be written to work on multiple types using type parameters.
    ```go
    func Index[T comparable](s []T, x T) int { ... }
    ```

    In addition, Go supports generic types.
    ```go
    type List[T any] struct {
        next *List[T]
            val T
    }
```

## Goroutines
A `goroutine` is a lightweight thread managed by the Go runtime.
    ```go
go f(x, y, z)
    ```

    starts a new goroutine running
    ```go
f(x, y, z)
    ```

    The evaluation of `x`, `y`, and `z` happens in the current goroutine and the 
    execution of `f` happens in the new goroutine.
    <br><br>

    Goroutines run in the same address sapce, so access to shared memory must be
    synchronized.
    The `sync` package provides usefule primitives.

### Channels
    Channels are a typed conduit through which you can send and receive values with
    the channel operator, `<-`.

    ```go
    ch := make(chan int)
    ch <- v // sends v to channel ch.
    v := <-ch // receive from ch
    ```

    By default, sends and receives block until the other side is ready.
    This allows goroutines to synchronize without explicit locks or condition
    variables.
    <br><br>

    Channels can be buffered. Sends to a buffered channel block only when the
    buffer is full. 
    Recieves block when the buffer is empty.
    ```go
    ch := make(chan int, 100)
    ```

    A sender can close a channel to indicate that no more values will be sent.
    Receivers can test whether a channel has been closed by assigning a second
    parameter.
    ```go
close(c)
    v, ok := <-ch

    ```
    `ok` is false if there are no more values to receive.
    Sending on a closed channel will cause a panic.

    ```go
    func fibonacci(n int, c chan int) {
        x, y := 0, 1
            for i := 0; i < n; i++ {
                c <- x
                    x, y = y, x+y
            }
        close(c)
    }

func main() {
c := make(chan int, 10)
       go fibonacci(cap(c), c)
       for i := range c {
           fmt.Println(i)
       }
}
```

### Select
A `select` statement lets a goroutine wait on multiple communication 
operations.

A `select` blocks until one of its cases can run, then it executes that case.
It chooses one at random if multiple are ready.
```go
var c, quit chan
for {
    select {
        case c <- x:
            // ...
        case <-quit:
            // ...
        default:
            // if no channels are ready. prevents blocking
    }
    ```

### sync.Mutex
        `sync.Mutex` has two methods: `Lock` and `Unlock`.
        ```go
        import "sync"

        type SafeCounter struct {
            mu sync.Mutex
                v map[string]int
        }

    func (c *SafeCounter) Inc(key string) {
        c.mu.Lock()
            defer c.mu.Unlock()

            c.v[key]++
    }
    ```

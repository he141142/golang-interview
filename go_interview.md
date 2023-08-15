# Golang basic:
## IN golang what happen If multiple goroutines access and modify the same global variable concurrently ?

DataRace: 

If multiple goroutines access and modify the same global variable concurrently without proper synchronization,
it can lead to data races. 
Data races occur when two or more goroutines access shared data simultaneously,
and at least one of them performs a write operation.
Data races can result in unpredictable and incorrect behavior.

## base:
### 1
Q: 
```
In Go, a string is a primitive type, which means it is read-only, and every manipulation of it will create a new string.

So if I want to concatenate strings many times without knowing the length of the resulting string, what's the best way to do it?
```
A: Beginning with Go 1.10 there is a strings.Builder. A Builder is used to efficiently build a string using Write methods. It minimizes memory copying. The zero value is ready to use.
How to efficiently concatenate strings in Go?

### What is zero value of interface type golang
In Go, the zero value of an interface type is nil. When an interface variable is declared without an explicit initialization, it is assigned the zero value, which for interfaces is nil.

An interface variable of zero value represents an interface with no underlying concrete type assigned to it. This means that the interface variable is not referencing any specific implementation or object. Attempts to access or invoke methods on a nil interface variable will result in a runtime error.

## GOLANG error handle
### Does golang support exception?

No, Go (often referred to as Golang) does not support traditional exceptions like some other programming languages such as Java or Python. Instead, Go uses a different error handling approach based on return values and explicit error checking.

In Go, functions typically return two values: a result and an error. The error value is used to indicate whether an operation was successful or if an error occurred. It is the responsibility of the calling code to check the error value and handle it appropriately.

### How can you create a custom error in Go? Why would you want to do that?
In Go, you can create a custom error by implementing the error interface. The error interface is defined as follows:
```go
type error interface {
    Error() string
}
```

To create a custom error, you need to define a new type that implements the error interface by implementing the Error() method. Here's an example:
```
type MyError struct {
    message string
}

func (e *MyError) Error() string {
    return e.message
}
```
### What is the purpose of the recover() function in Go?
In Go, the recover() function is used to regain control over a panicking goroutine (a concurrent part of a Go program) and allow it to gracefully handle a panic situation. It is typically used in conjunction with the defer statement to set up a recovery mechanism.

The purpose of the recover() function is to catch and handle panics within a limited scope, preventing them from propagating further and causing the program to terminate abruptly. By using recover(), you can regain control over the panicked goroutine and perform necessary cleanup tasks or take alternative actions.
## Interface
### What is the empty interface (interface{})?
In Go, the empty interface is denoted by the type interface{}. It is known as the empty interface because it does not specify any method. This means that an empty interface can hold values of any type since all types implicitly satisfy the empty interface.
### What are the properties of empty interface golang?

- Can hold values of any type: An empty interface can be used to hold values of any type. Since all types implicitly satisfy the empty interface, you can assign values of different types to an empty interface variable.

- No required methods: Unlike other interfaces in Go, the empty interface does not define any methods. It has no method signatures that types must implement. This makes it the most general interface in Go.

- Static type checking is bypassed: When using an empty interface, the static type checking of the Go compiler is bypassed. This means that you won't get compile-time type checking guarantees for the values assigned to an empty interface variable. The type information is checked dynamically at runtime instead.

- Limited operations: Since an empty interface doesn't have any methods defined, you can only perform a limited set of operations on an empty interface variable. You can assign values to it, check its type dynamically using type assertions or type switches, and compare it to nil for nil checks.

- Type assertions: To retrieve the value stored in an empty interface variable, you need to perform a type assertion to convert it back to its original type. This allows you to regain type-specific functionality for further use.
### How do you check if a value implements a specific interface in Go?
- Type Assertion:
```go
 var w Writer = FileWriter{}  // w is of type Writer interface

    fw, ok := w.(FileWriter)  // type assertion to check if w implements FileWriter interface
    if ok {
        // w implements FileWriter interface
        // fw is the underlying value of type FileWriter
        fw.Write("Hello, Go!")
```
- Type Switch:
```
func processValue(val interface{}) {
    switch v := val.(type) {
    case Writer:
        // val implements Writer interface
        v.Write("Hello, Go!")
    case Reader:
        // val implements Reader interface
        v.Read()
    default:
        // val does not implement any known interface
    }
}
```

## Name some advantages of Goroutines over threads

- Goroutines rất nhẹ so với luồng. Chúng chiếm ít bộ nhớ hơn và có áp lực hệ thống thấp hơn, cho phép bạn tạo và quản lý một số lượng lớn Goroutines mà không gây quá tải cho tài nguyên hệ thống.
- Goroutines sử dụng scheduler hiệu quả, cho phép đồng thời nhiều Goroutines chạy trên một số lượng nhỏ các thread . Điều này có nghĩa là bạn có thể chạy hàng ngàn hoặc thậm chí hàng triệu Goroutines cùng một lúc, tận dụng hiệu quả các corre CPU có sẵn mà không cần rieeng một thread cho mỗi Goroutine.
- Chi phí tạo và quản lý Goroutines thấp hơn nhiều so với luồng. Tạo một Goroutine chỉ đơn giản như một cuộc gọi hàm, và chúng yêu cầu ít bộ nhớ. Điều này cho phép tạo Goroutines cho các nhiệm vụ nhỏ hoặc xử lý một số lượng lớn yêu cầu đồng thời mà không phải lo lắng về việc tiêu thụ tài nguyên quá mức.
- Goroutines trong Go giao tiếp và đồng bộ hóa sử dụng channels, cung cấp cách an toàn và hiệu quả để trao đổi dữ liệu giữa các Goroutines. Channels giúp điều phối và chia sẻ thông tin giữa các Goroutines, làm cho việc viết mã đồng thời và song song dễ dàng hơn mà không phải lo về cơ chế lock hoặc data race

## Given the code bellow:

```go

```


##  How to check if a map contains a key in Go?
# Most challenging project with golang? (cách này cố kéo dài thời gian)
# Framework/lib you work in golang?
- orm: Gorm, Ent go
- rest-api: gin, chi
- graphql: gqlgen
- test: gocheck, go vet,Testify,GoConvey



# Do you Know about 10k,100K problems? How Can you handle ?
- Cái này tổng hợp những kinh nghiệm mà mình đã làm:
  - từ quản lí code base sao cho hiệu quả (follow clean , onion architecture)
  - Turning Sql , Đặt index sao cho hiệu quả, cách dùng select(chỉ select các cột cần thiết)
  - Profiling and Monitoring (giám sát tốc độ truy vẫn , execution plan) => nếu cần cải thiện có thể truy ra bottlenect và viết lại truy vấn
  - Caching: (chọn strategy phù hợp cho hệ thống heavy write or heavy read? Traffic workload?)
    - Write-through cache:
        - Prop:  Fast retrieval, complete data consistency between cache and storage.
        - Cons: Higher latency for write operations.
    - Write-around cache:
        - prop:  reduce latency.
        - cons: increases cache misses because the cache system has to read the information from the database in case of a cache miss. As a result, this can lead to higher read latency in the case of applications that write and re-read the information quickly
    - Write-back cache: 
      - prop:  reduced latency and high throughput for write-intensive applications
      - cons: risk of data loss in case the caching layer crashes -> resolve: having more than one replica acknowledging the write in the cache.
  - Denormalize database (giảm việc tách bảng, thay vào đó gộp các bảng lại với nhau nếu được để giảm tải lưu lượng read cho database)

- Chiến lược phân tán database:
    + Federation
    + Master Slave database
    + Partitioning/Sharding
- Kiểm tra datarace: sử dụng `-race` FLAG

- Câu thêm time bằng cách chém gió về các chiến lược triển khai testing, xác định bottleneck, issue detection:
```text
Unit Testing:  ensure that individual functions and components work as expected. (smallest unit)
Integration Testing: Perform integration tests to validate that different parts of your application work together correctly. This helps catch issues that may arise when components interact.( Kiểm tra khi mà các components trong app đã thực sự liên kết với nhau...)
Automated Testing: Set up automated testing pipelines that run tests on every code commit. This ensures that new code doesn't introduce regressions or break existing functionality.
Code Review: Conduct thorough code reviews to catch potential issues early. Code reviews also help ensure that code adheres to best practices and coding standards.
Benchmarking: Utilize benchmark tests to measure the performance of critical functions or components. Benchmark tests provide insights into how changes affect the performance of your code.
Static Analysis: Employ static analysis tools like golint and go vet to catch potential issues and ensure code quality.
Load Testing: Simulate high traffic scenarios to identify bottlenecks and ensure your application can handle a large number of concurrent users.
Logging & monitoring
```


## Deep dive on benchmark:
Separating benchmarking by level, running benchmarks, sub-benchmarks, subtests, support for test skipping, and support for test setup and teardown.
- Unit-Level Benchmarking: Benchmark individual functions or small code units to measure their performance in isolation. This helps you understand the performance characteristics of critical code paths.
- Integration-Level Benchmarking: Benchmark interactions between components or subsystems to ensure that the system as a whole meets performance requirements.

Running Benchmarks: `go test -bench=.`
Sub-Benchmarks: benchmark different cases of a function with varying inputs.
Subtests: used for testing and benchmarking multiple scenarios within a single test function. They provide more context and flexibility.
(chia sub test ra riêng module sau đó nhét vào 1 array rồi chạy hết 1 lần duy nhất,có thể chia ra làm module riêng)
```text
func BenchmarkMyFunction(b *testing.B) {
    tests := []struct {
        name   string
        input  int
        output int
    }{
        {"Case1", 1, 2},
        {"Case2", 2, 4},
    }

    for _, test := range tests {
        b.Run(test.name, func(b *testing.B) {
            for i := 0; i < b.N; i++ {
                result := MyFunction(test.input)
                if result != test.output {
                    b.Fatalf("expected %d, got %d", test.output, result)
                }
            }
        })
    }
}
```



# Choosing Sql or NoSql?
- CAP theorem
- ACID properties
- Why?

# CI/CD flow? How you work with it?
...
# Do you know graphql? How do you work with it?
...
# Why golang fast? Different between golang compiler and java?
- Java sử dụng trình biên dịch Just-In-Time (JIT), biên dịch mã nguồn thành mã trung gian bytecode (.class files), sau đó chuyển đổi bytecode thành mã máy trong quá trình chạy.
- Golang: Go sử dụng trình biên dịch tĩnh, biên dịch mã nguồn Go thành mã máy trực tiếp. Không có bước tạo mã trung gian nào.
# Different between golang and other language ( How much you know about golang? )...
Nêu những ý chính:

- Simple and Understandable: Go is very simple to learn and understand. There are no unnecessary features included. Every single line of the Go code is very easily readable and thereby easily understandable irrespective of the size of the codebase. Go was developed by keeping simplicity, maintainability and readability in mind.
- Standard Powerful Library: Go supports all standard libraries and packages that help in writing code easily and efficiently.
- Support for concurrency: Go provides very good support for concurrency using Go Routines or channels. They take advantage of efficient memory management strategies and multi-core processor architecture for implementing concurrency.
- (quan trọng) Static Type Checking: Go is a very strong and statically typed programming language. Statically typed means every variable has types assigned to it. The data type cannot be changed once created and strongly typed means that there are rules and restrictions while performing type conversion. This ensures that the code is type-safe and all type conversions are handled efficiently.
- This is done for reducing the chances of errors at runtime.
- Easy to install Binaries: Go provides support for generating binaries for the applications with all required dependencies. These binaries help to install tools or applications written in Go very easily without the need for a Go compiler or package managers or runtimes.
- Good Testing Support: Go has good support for writing unit test cases along with our code. There are libraries that support checking code coverage and generating code documentation.
- Well Scaled: The Go language has Goroutines, which are basically functions that can run simultaneously and independently.

Goroutines take up only 2 kB of memory, which makes it scalable when the need for running multiple concurrent processes arise. Unlike Java threads, which are blocking by nature, Goroutines are non-blocking. Goroutines is the combination of async approach used by JavaScript and the traditional multi-threading used by Java.

Golang’s Goroutines are the opposite of what Java’s thread is, where the latter is a heavyweight that gobbles up memory. Technically, you can run millions of GoRoutines without crashing the system. Having a leaner and meaner software gives you an edge over your competitors. 


#Cracking the code Interview GOLANG
1. Given function:
```go
      func(input interface{})error{}
```

Q: How To Specify the Type of input ?
2. Give json file:

```json
{
  "dateOfBirth": "2020-12-06",
  "UserName": "John",
  "Age": 22
}
```

And the struct type:
```go
type Person struct{
	DateOfBirth *time.Time 
	Name string
	Age int
}
```

Q: Using `json.Unmarshal` from package `encoding/json`
To bind json to struct
Note that you can modify the struct if you want
but the json file is fixed

3.How to **Save** your application from *panic* call?

<br>
4. Consider scenario:
You have a list of task before start up the server:
    - Cronjob
    - Clear log files
    - Send notification to user
    - Clear cache data from redis


<br>
All of them are represented as bellow:

`cronjob.go`:
```go
type Cronjob struct {
	Schedule time.Duration
}

func (job *Cronjob)RunCronjob(){
	//implement logic
}
```
`clear_log.go`:
```go
type ClearLogJob struct {
	Schedule time.Duration
	Directory string
}

func (job *ClearLogJob)RunClearLogJob(){
	//implement logic
}
```

`clear_cache.go`:
```go
type ClearCache struct {
	RedisClient *redis.Client
	Keys        []string
}

func (job *ClearCache)RunClearCache(){
	//implement logic
}
```

...etc

Q:How to push all of them to a slice and execute the job by iterating through the slice?


5. Implement Constructor of a struct and ensure it can be initialized **ONLY ONE TIME**
   (Can call this constructor multiple time but the struct must have to be initialized only one time)

6.Implement Builder pattern In golang?

7.How to prevent unKeyed literals for struct in golang?
Example this code: 
```go
type Person struct {
    Name string
    Age  int
}
func main() {
    // Incorrect: Unkeyed literals
    p1 := Person{"John Doe", 30}
    
    // Correct: Named fields
    p2 := Person{Name: "John Doe", Age: 30}
    
    fmt.Println(p1)
    fmt.Println(p2)
}
```
How to Force struct `Person` is not able to use Unkeyed literals?



## Overview
- Go is a compiled language with low memory usage.
- The Go runtime handles memory management.
- It is compiled faster than other compiled languages, and runs faster than interpreted languages.
	- Compiled programs do not need access to source code when running, meaning there are no runtime language dependencies when deployed.
![[languages.png]]
1. `package main` lets the Go compiler know that we want this code to compile and run as a standalone program, as opposed to being a library that's imported by other programs.
2. `import fmt` imports the `fmt` (formatting) package. It is Go's standard library.
3. `func main()` defines the `main` function.

## Variables
- Go enforces strong and static typing, meaning a variable cannot change type.
### Types
	- bool
	- string
	- int, int8, int16, int32, int64
	- uint, uint8, uint16, uint32, uint64, uintptr
	- byte                  // alias for uint8
	- rune                  // alias for int32, represents a Unicode point
	- float32, float64
	- complex64, complex128 // imaginary numbers
#### Defaults
	- bool
	- string
	- int
	- uint32
	- byte
	- rune
	- float64
	- complex128

### Declarations
```Go
var number int
var pi float64 = 3.14159
text := "Sample Text"              // short variable declaration inferrs type
					               // cannot be used for global vars
g := 0.867 + 0.5i                  // type inferrence = complex 128
mileage, company := 80276, "Tesla" // multiple var declarations
```

### Constants
```Go
const planName = "Basic Plan"
const fullName = firstName + " " + lastName // constants can be concatenated
const seconds = minutes * hour              // constants can be computed
const (
	string1 = "abcd"
	string2 = "efgh"
	string3 = "ijkl"
)
```

### Type Casting
```Go
temperatureFloat := 88.26
temperatureInt := int64(temperatureFloat)
```
- 2 unalike types cannot be computed.
- For example, an integer cannot be multiplied with a float, so a cast is required
```Go
// float     // int casted to float  
.05       *   float64(5)
```

### Concatenation
- Cannot concatenate string and numeric variables.
```Go
var username string = "wagslane"
var password string = "20947382822"

fmt.Println("Authorization: Basic", username+":"+password)
```

### String Formatting
- fmt.Printf() - Prints a formatted string to standard out
```Go
fmt.Println()
```
- fmt.Sprintf() - Returns the formatted string
```Go
msg := fmt.Sprintf("Hi %s, your open rate is %.1f percent\n", name, openRate)
s := fmt.Sprintf("I am %.2f years old", 10.523)
```
	- %v - any value
	- %s - string
	- %d - decimal
	- %f - float

### String Comparison
```Go
string1 == string2
```
## Conditionals
### If, Else
- No parenthesis around conditional
```Go
if height > 6 {
    fmt.Println("You are super tall!")
} else if height > 4 {
    fmt.Println("You are tall enough!")
} else {
    fmt.Println("You are not tall enough!")
}
```
- Can add initial statement before conditional to limit scope
```Go
if length := getLength(email); length < 1 {
    fmt.Println("Email is invalid")
}
```

### Switch, Case
```Go
switch {
	case :
	case :
	default:
}
```

### Comparison Operators
	- ==
	- !=
	- <, >
	- <=, >=

## Functions
- `func sub(x int, y int) int` is known as the "function signature".
```Go
func sub(x int, y int) int {
  return x-y
}
```
- Multiple arguments of the same type can share a declaration
```Go
func sub(x, y int) int
```
- Function overloading:
```Go
func addToDatabase(hp, damage int)
func addToDatabase(hp, damage int, name string)
func addToDatabase(hp, damage int, name string, level int)
```
- Below is a function named 'f' that takes a function and an int as arguments and returns an int. https://www.geeksforgeeks.org/higher-order-function-in-golang/
```Go
f func(func(int,int) int, int) int
```

### Multiple Return Values
- A function can have multiple return values
```Go
func getPoint() int             // returns 1 int
func getPoint() (int, int)      // returns 2 int
func getPoint() (int, int, int) // returns 3 int
```

### Ignore Return Values
- The compiler will throw an error if you have unused variable declarations. So you can ignore a returned value if you have no use for it.
```Go
func getPoint() (x int, y int) {
  return 3, 4
}
// ignore y value
x, _ := getPoint()
```

### Named Return Values
```Go
func getCoords() (x, y int){  // this is a naked return
return // automatically returns x and y
}
```
- Is the same as:
```Go
func getCoords() (int, int) { // this is a named return
var x int
var x int
return x, y
}
```
- It is better convention to explicitly return values:
```Go
func getCoords() (x, y int) {
return x, y
}
```

### Early Returns/Guard Clauses
- Guard Clauses are early return from a function when a condition is met.
```Go
func divide(dividend, divisor int) (int, error) {
	if divisor == 0 {
		return 0, errors.New("Can't divide by zero")
	}
	return dividend/divisor, nil
}
```

## Structs
- Structs can be nested.
```Go
type car struct {
	Make string
	Model string
	FrontWheel Wheel
	BackWheel Wheel
}
type Wheel struct {
	Radius int
	Material string
}
```
- create a variable using the struct
```Go
myCar := car{}
myCar.FrontWheel.Radius = 5

car2 := {
	Make: "Mazda",
	Model: "CX3",
	FrontWheel: Wheel{
		Radius: 17,
		Material: "Aluminum"
	}
}
```

### Anonymous Struct
- 1 time use struct
```Go
myCar := struct {  // This creates a struct
	Make string
	Model string
} {                // This uses the struct
	Make: "tesla",
	Model: "model 3",
}
```
- Can do this with nested struts as well
```Go
type car struct {
	Make string
	Model string
	Wheel struct { // This is the anonymous nested struct
		Radius int
		Material string
	}
}
```

### Embedded Structs
- A struct that contains an embedded struct inherits the fields of that struct
```Go
type car struct {
  make string
  model string
}

type truck struct { // 'truck' now contains the fields of 'car'
  car
  bedSize int
}
```

### Receiver Function
- A receiver is a special kind of function parameter. They are methods that can run by structs.
```Go
type rect struct {           // struct defined
  width int
  height int
}
func (r rect) area() int {   // area has a receiver of (r rect)
  return r.width * r.height
}
r := rect{                   // struct instantiated
  width: 5,
  height: 10,
}
fmt.Println(r.area())        // method run by var
```

## Interfaces
- Interfaces in Go are implicit, meaning we don't have to explicitly write that a struct implements an interface.
- Interfaces in Go are collections of method signatures.
```Go
type shape interface {   // interface requires these 2 methods
	area() float64
	perimeter() float64
}
```
- Multiple structs can implement the same interface
```Go
type rect struct {
	width, height float64
}
type circle struct {
	radius float64
}

func (r rect) area() float64 {   // receiver function
	return r.width * r.height
}
func (c circle) area() float64 { // receiver function
	return c.radius * c.radius * math.Pi
}
```
- We can use interfaces to call methods from all the implemented structs
- This means that we can pass any struct into a function as long as the interface is implemented
```Go
func printArea(s shape) {
	fmt.Println(s.area())
}
```

### Multiple Interfaces
- A type can implement multiple interfaces.
```Go
type expense interface { // interfaces
	cost() float64
}
type printer interface {
	printOut()
}

type email struct {      // struct
	isSubscribed bool
	body string
}

func (e email) cost() float64 { // receiver function for expense interface
	if !e.isSubscribed {
		return float64(len(e.body)) * .05
	}
	return float64(len(e.body)) * .01
}
func (e email) printOut {       // receiver function for printer interface
	fmt.Println(e.body)
}

func compute(e expense, p printer) { // function accepting interfaces as arguments
	fmt.Printf("This is the cost: %.2f \n", e.cost())
	p.printOut()
}

func main() {
	mail := email {      // instantiating struct
		isSubscribed: true,
		body: "Test Message"
	}
	compute(mail, mail)  // sending the same struct into both interface arguments
}
```

### Sub Interface
- Just like embedded structs, you can embed interfaces to get sub interfaces.
- In this example the 'firetruck' interface inherits all of the methods within the 'car' interface.
- You would use this if you have a special case that needs extra methods attached.
```Go
type car interface {
	Color() string
	Speed() int
}
type firetruck interface {
	car
	HoseLength() int
}
```

### Named Interface Arguments
```Go
type Copier interface {
  Copy(sourceFile string, destinationFile string) (bytesCopied int)
}
```
- Is better convention than this:
```Go
type Copier interface {
  Copy(string, string) int
}
```

### Type Assertions
- Type assertions are basically casts done on an interface to receive the underlying struct
```Go
// "c" is a new circle cast from "s"
// which is an instance of a shape.
// "ok" is a bool that is true if "s" was a circle
// or false if "s" isn't a circle.
c, ok := s.(circle)
if !ok {
	// s wasn't a circle
	log.Fatal("s is not a circle")
}
```

### Type Switches
- Type switches allow you to do several type assertions in the form of a switch statement.
```Go
func test(e expense) { // e is the interface, email and sms are the structs
	address, cost := getExpenseReport(e)
	switch e.(type) {
	case email:
		fmt.Printf("Report: The email going to %s will cost: %.2f\n", address, cost)
		fmt.Println("====================================")
	case sms:
		fmt.Printf("Report: The sms going to %s will cost: %.2f\n", address, cost)
		fmt.Println("====================================")
	default:
		fmt.Println("Report: Invalid expense")
		fmt.Println("====================================")
	}
}
```

### General Advice
- Keep interfaces small, they are meant to define the minimal behavior necessary.
- Interfaces are not classes.
- Interfaces define function signatures, but not underlying behavior.

## Errors
- Error handling works similarly to type assertions.
- Every function call in Go returns an error, although if it's a safe function that error is nil.
```Go
user, err := getUser()
if err != nil {
	fmt.Println(err)
	return
}
profile, err := getUserProfile(user.ID)
if err != nil {
	fmt.Println(err)
	return
}
```
- To return an error from a dangerous function, you can send an error out directly from the function using the error format specifier.
```Go
func sendSMS(message string) (float64, error) { // error interface built-in type
	const maxTextLen = 25
	const costPerChar = .0002
	if len(message) > maxTextLen {
		return 0.0, fmt.Errorf("can't send texts over %v characters", maxTextLen)
	} // Errorf() error format specifier
	return costPerChar * float64(len(message)), nil
}
```

### Structs Implementing Error Interface
- Any struct can have a custom error by implementing the error interface
```Go
type error interface {
	Error() string
}
```
- Any struct, as long as it implements the error interface, can throw an error.
```Go
type divideError struct { // struct
	Dividend float64
}
func (de divideError) Error() string { // receiver function implements error interface
	return fmt.Sprintf("an not divide %.2f by zero", de.Dividend)
}
func divide(divident, divisor float64) (float64, error) {
	if divisor == 0 {
		return 0.0, divideError{Dividend: dividend}
	} // if there is an error, create a struct that returns an error because it implements the error interface
	return dividend/divisor, nil
}
```

### Errors Package
- If you don't need error formatting or a struct specific error, then you can use the errors package to return a simple error:
```Go
import {
	"errors"
	"fmt"
}
func divide(x, y float64) (float64, error) {
	if y == 0 {
		return 0.0, errors.New("no dividing by 0")
	}
	return x/y, nil
}
```

## Loops
### For Loop
```Go
for i := 0; i < 10; i++ {
	fmt.Println(i)
}
```

### Condition-less For loop
- If you want to run an endless loop, omit the condition. 
```Go
for INITIAL; ; AFTER {
  // do something forever
}
```

### No While Loop
- There is no while loop in Golang, just use a for loop.
```Go
plantHeight := 1
for plantHeight < 5 {
	fmt.Println("still growing! current height:", plantHeight)
	plantHeight++
}
fmt.Println("plant has grown to ", plantHeight, "inches")
```

### For Each Loop
```Go
func twoSum(nums []int, target int) []int {
	for index, value := range nums {              // for each loop
		for i := index + 1; i < len(nums); i++ {  // regular for loop through an array
			if value+nums[i] == target {
				return []int{index, i}
			}
		}
	}
	return []int{}
}
```

### Logical Operators
	- &&
	- ||
	- %

### Continue and Break
- Continue - if you want to skip a loop iteration
- Break - if you want to exit the loop

## Arrays and Slices
### Arrays
- Arrays are fixed in size
```Go
var arr [10]int          // array declaration
arr := [5]int{1,2,4,8,0} // initialized literal
return [5]int{1,2,4,8,0} // returns the array literal

fmt.Printf("Int at index 3: %d", arr[3]) // retreives from array
fmt.Printf("Array has a length of %d", len(arr)) // len() returns the max size
```

### Slices
- Slices are built on arrays, think of them as a sub-array
```Go
primes := [6]int{2, 3, 5, 7, 11, 13}
mySlice := primes[1:4] // subarray of the range, lowIndex to highIndex-1
// mySlice = {3, 5, 7}
```
- Syntax:
```Go
arrayname[lowIndex:highIndex]
arrayname[lowIndex:]
arrayname[:highIndex]
arrayname[:] // uses the entire array
```

### Slice Literal
- Slice literals are similar to arraylists, as you add values to it the size increases.
- You can create a slice directly without dealing with the underlying array
```Go
// func make([]T, len, cap) []T
mySlice := make([]int, 5, 10)
// the capacity argument is usually omitted and defaults to the length
mySlice := make([]int, 5)
// you can also create an empty slice with literals
mySlice := []int{}
```
- A slice literal is created when you don't add a max length to the declaration
```Go
mySlice := []string{"I", "love", "go."} // if you add 3 in the brackets, you create an array instead of a slice
fmt.Println(len(mySlice)) // len() returns the number of elements
fmt.Println(cap(mySlice)) // cap() returns the max size of the underlying array
                          // before reallocation of the array is necessary
```

### Modifying a Slice
- If you make a slice that is a sub-array then any time you make changes to the slice, it changes the underlying array. This does not change the length of the array but it does change the length of the slice.
```Go
primes := [6]int{2, 3, 5, 7, 11, 13}
slice := primes[1:4] // [3 5 7]

slice = append(slice, 17)
fmt.Printf("The array is %v\n", primes) // [2 3 5 7 17 13]
fmt.Printf("The new slice is %v\n", slice) // [3 5 7 17]
```

### Variadic Functions
- Variadic functions receive an arbitrary number of arguments and treats them as a slice.
```Go
func sum(nums ...int) int {
	sum := 0
	for _, num := range nums {
		sum += num
	}
	return sum
}
func main() {
	fmt.Print(sum(1,5,2,6,7,2,3))
}
```
#### Spread Operator
- The spread operator allows a slice to be passed into a Variadic function
```Go
func printStrings(strings ...string) {
	for i := 0; i < len(strings); i++ {
		fmt.Println(strings[i])
	}
}
func main() {
    names := []string{"bob", "sue", "alice"}
    printStrings(names...)
}
```
### Append
- The append() function changes the underlying array of it's parameter AND returns a new slice. This means that using the append() function on anything other than itself is a bad idea.
```Go
slice = append(slice, firstElement)
slice = append(slice, firstElement, secondElement)
slice = append(slice, anotherSlice...)

// you can also add elements regularly
costs[index] = float64(len(message)) * .01
```
- The append() function only creates a new array then there isn't any capacity left. This means that if an array has space left in it to be allocated then any append function will return a slice from the same memory address and overwrite any previous appends.
```Go
i := make([]int, 3, 8)
j :- append(i, 4)
fmt.Println("addr of j: ", &j[0]) // addr of j: 0x454000
k :- append(i, 5)
fmt.Println("addr of k: ", &k[0]) // addr of k: 0x454000
```
### 2D Slices/Matrix
```Go
func createMatrix(rows, cols int) [][]int {
	matrix := make([][]int, 0) // makes a slice of length 0
	for i := 0; i < rows; i++ { // loops the outer slice
		row := make([]int, 0) // makes a slice of length 0
		for j := 0; j < cols; j++ { // loops the inner slice
			row.append(row, i*j) // adds elements to the inner slice
		}
		matrix = append(matrix, row) // adds the inner slice to the outer slice
	}
	return matrix
}
```

## Maps
- Maps key->value
```Go
ages := make(map[string]int) // map using make()
ages["John"] = 37
ages["Mary"] = 24
ages["Mary"] = 21 // overwrites 24

ages = map[string]int{ // literal map
  "John": 37,
  "Mary": 21,
}

len(ages) // returns number of key/value pairs
age = ages["Mary"] // get an element, age = 21
```
-  A map can have keys for any type that is comparable. This includes structs. This is also includes nested maps (map of maps).
```Go
type user struct { // user struct
	name string
	phoneNumber int
}
// map[string]user
users[names[i]] = user{
	name: names[i],
	phoneNumber: phoneNumbers[i],
}
```
- This is an example of an efficient struct key:
```Go
type Key struct {
    Path, Country string
}
hits := make(map[Key]int)

// When a Vietnamese person visits the home page, incrementing (and possibly creating) the appropriate counter is a one-liner:
hits[Key{"/", "vn"}]++

// And it’s similarly straightforward to see how many Indian people have read the spec:
n := hits[Key{"/ref/spec", "in"}]
```

### Mutations
```Go
delete(m, key) // deletes key from map m

elem, ok := m[key] // if key is in m, ok=true

if attended[person] { // will be false if person is not in the map
    fmt.Println(person, "was at the meeting")
}
```

### Nested Maps
```Go
map[string]map[string]int         // double nest
map[int]map[string]map[string]int // triple nest
```
- Example of this:
```Go
func getNameCounts(names []string) map[rune]map[string]int {
	nameCount := make(map[rune]map[string]int)
	for _, name := range names {
		if name == "" {
			continue
		}
		if nameCount[rune(name[0])] == nil {
			nameCount[rune(name[0])] = make(map[string]int)
		}
		nameCount[rune(name[0])][name]++
	}
	return nameCount
}
```

## First Class and Higher Order Functions


## Pointers


## Local Development
### Packages
- Golang import only needs to be done if the files are not within the same directory.
- This also means that multiple packages cannot live within the same directory.

## Channels


## Mutexes


## Generics




// temporary note on how to link sections from one note to another. 
// can use this to create individual notes for algorithm implementation in different languages, and link them back to a master note, that explains the algo itself.
![[Algorithms#Binary Search]]
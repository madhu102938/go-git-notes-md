`var arr [4]int`
```go
planets2 := [...]string{ 
	"Mercury",
	"Venus",
	"Earth",
	"Mars",
	"Jupiter",
	"Saturn",
	"Uranus",
	"Neptune",// last comma is required
} 

planets2 := [...]string{ 
	"Mercury",
	"Venus",
	"Earth",
	"Mars",
	"Jupiter",
	"Saturn",
	"Uranus",
	"Neptune"} // comma not required 

random(names, // comma required
)

random(names) // commna not required
```

# Slices
In Go, both array slicing and string slicing create new slices or substrings that reference the original data. However, there are some nuances to understand regarding how they work:

### Array Slicing

- **Pass by Reference**: When you create a slice from an array or another slice, the new slice references the same underlying array. Changes to the elements of the slice will affect the original array.
- **Example**:

  ```go
  package main

  import "fmt"

  func main() {
      arr := [5]int{1, 2, 3, 4, 5}
      slice := arr[1:4] // slice references elements 2, 3, 4 of arr

      fmt.Println("Original array:", arr)
      fmt.Println("Slice:", slice)

      slice[0] = 10 // modifies the original array
      fmt.Println("Modified array:", arr)
      fmt.Println("Modified slice:", slice)
  }
  ```

  Output:
  ```
  Original array: [1 2 3 4 5]
  Slice: [2 3 4]
  Modified array: [1 10 3 4 5]
  Modified slice: [10 3 4]
  ```

### String Slicing

- **Pass by Reference**: When you create a substring from a string, the new substring references the same underlying string data. However, strings in Go are immutable, so you cannot modify the original string through the substring.
- However, you can assign a new string to the variable holding the substring. This does not change the original string or the original substring; it simply makes the variable reference a new string.
- **Example**:

  ```go
  package main

  import "fmt"

  func main() {
      str := "hello world"
      substr := str[1:5] // substr references "ello"

      fmt.Println("Original string:", str)
      fmt.Println("Substring:", substr)

      // Attempting to modify the substring will result in a compilation error
      // substr[0] = 'a' // error: cannot assign to substr[0]
  }
  ```

  Output:
  ```
  Original string: hello world
  Substring: ello
  ```

### Summary

- **Array Slicing**: Creates a new slice that references the same underlying array. Changes to the slice affect the original array.
- **String Slicing**: Creates a new substring that references the same underlying string data. Strings are immutable, so you cannot modify the original string through the substring.

In both cases, slicing creates a new view into the original data, but the behavior differs due to the mutability of arrays and the immutability of strings.

```go
package main

import (
	"fmt"
)

func main() {
	planets := [...]string{
		"Mercury",
		"Venus",
		"Earth",
		"Mars",
		"Jupiter",
		"Saturn",
		"Uranus",
		"Neptune",
	}

	terra := planets[:4]
	iceGaint := planets[6:]
	myPlanet := terra[2:3]
	 
	fmt.Println(planets)
	fmt.Println(terra, gasGaint, iceGaint)
	fmt.Println(myPlanet)

/*
[Mercury Venus Earth Mars Jupiter Saturn Uranus Neptune]
[Mercury Venus Earth Mars] [Jupiter Saturn] [Uranus Neptune]
[Earth]
*/
}
```

- Slices are passed by reference by default
```go
package main

import (
	"fmt"
)

func changingSlice(names []string) {
	for i, name := range names {
		if name == "Pluto" {
			names[i] = "Hehe smol rock"
		}
	}
}

func main() {
	// initializing a slice
	names := []string{"Ceres", "Pluto", "Haumea", "Makemake", "Eris"}

	fmt.Println(names)
	changingSlice(names)
	fmt.Println(names)
}

/*
[Ceres Pluto Haumea Makemake Eris]
[Ceres Hehe smol rock Haumea Makemake Eris]
*/
```

**Summary**
- Slices have a length and a capacity. 
- When there isn’t enough capacity, the built-in append function will allocate a new underlying array. 
- You can use the make function to pre-allocate a slice. 
- Variadic functions accept multiple arguments, which are placed in a slice.

# Maps

### Summary

- **Arrays**: Copied when passed to functions or assigned to variables.
- **Slices**: Reference types; modifications affect the original slice.
- **Maps**: Reference types; modifications affect the original map.
- **Structs**: Copied when passed to functions or assigned to variables, but fields that are reference types will reference the same underlying data.
- **Pointers**: Reference types; modifications affect the original data.

Understanding these behaviors helps you manage data and avoid unintended side effects in your Go programs.

```go
func make(t Type, size ...int) Type
```

The `make` built-in function allocates and initializes an object of type `slice`, `map`, or `chan` (**only**). Like new, the first argument is a type, not a value. Unlike `new`, make's return type is the same as the type of its argument, **not** a pointer to it. The specification of the result depends on the type:

**Summary**
- Maps are versatile collections for unstructured data. 
- Composite literals provide a convenient means to initialize maps. 
- The range keyword can iterate over maps. 
- Maps share the same underlying data when assigned or passed to functions.
- Keys in map are not stored in any particular order (`unordered_map` maybe)







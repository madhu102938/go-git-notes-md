# `strings.FieldFunc`
#### func [FieldsFunc](https://cs.opensource.google/go/go/+/go1.23.2:src/strings/strings.go;l=382) [¶](https://pkg.go.dev/strings#FieldsFunc)

`func FieldsFunc(s string, f func(rune) bool) []string `

`FieldsFunc` splits the string s at each run of Unicode code points c satisfying f(c) and returns an array of slices of s. If all code points in s satisfy  `f(c)` or the string is empty, an empty slice is returned.

`FieldsFunc` makes no guarantees about the order in which it calls f(c) and assumes that f always returns the same value for a given c.

When you want to split the string at whitespaces, then we can directly use `strings.Fields` it only takes a `string` and outputs `[]string`

```go
package main

import (
	"fmt"
	"strings"
)

func main() {
	sentence := "hello how are you doing :)"
	f := func(ch rune) bool {
		return string(ch) == " "
	}
	words := strings.FieldsFunc(sentence, f)
	for _, v := range words {
		fmt.Println(v)
	}
}
```
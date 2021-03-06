# crunch

[![godoc](https://godoc.org/github.com/superwhiskers/crunch?status.svg)](https://godoc.org/github.com/superwhiskers/crunch)&nbsp;[![travis](https://travis-ci.org/superwhiskers/crunch.svg?branch=master)](https://travis-ci.org/superwhiskers/crunch#)&nbsp;[![codecov](https://codecov.io/gh/superwhiskers/crunch/branch/master/graph/badge.svg)](https://codecov.io/gh/superwhiskers/crunch)&nbsp;[![go report card](https://goreportcard.com/badge/github.com/superwhiskers/crunch)](https://goreportcard.com/report/github.com/superwhiskers/crunch)&nbsp;[![edit on repl.it](https://img.shields.io/badge/try%20it%20on-repl.it-%2359646A.svg)](https://repl.it/github/https://github.com/superwhiskers/crunch?ref=button)


manipulate bytes and bits in golang with ease

## install

```
$ go get github.com/superwhiskers/crunch
```

## benchmarks

`MiniBuffer` performs on average more than twice as fast as `bytes.Buffer` in both writing and reading
```
BenchmarkBufferWrite-4          	30000000	         47.6 ns/op	       0 B/op	       0 allocs/op
BenchmarkBufferRead-4           	20000000	         111 ns/op	       0 B/op	       0 allocs/op
BenchmarkMiniBufferWrite-4      	200000000	         7.29 ns/op	       0 B/op	       0 allocs/op
BenchmarkMiniBufferRead-4       	1000000000	         1.73 ns/op	       0 B/op	       0 allocs/op
BenchmarkStdByteBufferWrite-4   	50000000	         24.6 ns/op	       0 B/op	       0 allocs/op
BenchmarkStdByteBufferRead-4    	200000000	         7.84 ns/op	       0 B/op	       0 allocs/op
```

## example

```golang
package main

import (
	"fmt"
	"github.com/superwhiskers/crunch"
)

func main() {

	// creates a new buffer with four zeroes
	buf := crunch.NewBuffer([]byte{0x00, 0x00, 0x00, 0x00})
	
	// write the byte `0x01` to the first offset, and move the offset forward one
	buf.WriteByteNext(0x01)
	
	// write the byte `0x01` to the second offset, and move the offset forward one
	buf.WriteByteNext(0x01)
	
	// seek the offset back one
	buf.Seek(-1, true)
	
	// write the bytes `0x02` and `0x03` to the second and third offsets, respectively
	buf.WriteBytesNext([]byte{0x02, 0x03})
	
	// write the byte `0x04` to offset `0x03`
	buf.WriteByte(0x03, 0x04)
	
	// output the buffer's contents to the console
	fmt.Printf("%v\n", buf.Bytes())
	
}
```

## license

[lgplv3](https://www.gnu.org/licenses/lgpl-3.0.en.html)

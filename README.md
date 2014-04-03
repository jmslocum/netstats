# netstats.go

A Go interface to the /proc/net/dev file. All major Linux distributions 
use procfs and report system details through various dynamically generated 
files. This library will read the network stats reported by the kernel for 
all devices on the system and build a slice of data structures. 

## Installation

To install the package from github, run the command
`go get github.com/jmslocum/netstats`

## Usage

```Go
package main

import (
	"fmt"
	"github.com/jmslocum/netstats"
	"net"
)

func main() {
	//Get stats for all interfaces on system
	allStats, err := netstats.Stats()
	if err != nil {
		panic(err)
	}

	for _, s := range(allStats) {
		fmt.Printf("%v\n", s)
	}

	//Get stats for a specific device by name
	stats, err := netstats.StatsByName("lo")
	if err != nil {
		panic(err)
	}

	fmt.Printf("%v\n", stats)

	//Get stats for a speciic device by net.Interface
	iface, err := net.InterfaceByName("eth0")
	if err != nil {
		panic(err)
	}

	stats, err = netstats.StatsByInterface(iface)
	if err != nil {
		panic(err)
	}

	fmt.Printf("%v\n", stats)
}
```

## License

Copyright (C) 2014 James Slocum (jamesslocum.com)


Permission is hereby granted, free of charge, to any person obtaining a copy 
of this software and associated documentation files (the "Software"), to deal 
in the Software without restriction, including without limitation the rights 
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies 
of the Software, and to permit persons to whom the Software is furnished to do 
so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all 
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, 
INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A 
PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT 
HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF 
CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE 
OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## See Also

I have a similar library written in C [here on github](https://github.com/jmslocum/ifstats)

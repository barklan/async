# async go fork

**Uses [`golang.org/x/sync/errgroup`](https://pkg.go.dev/golang.org/x/sync/errgroup) internally. API is not changed.**

```go
package main

import (
	"context"
	"fmt"
	"log"
	"time"

	"github.com/barklan/async"
)

type User struct {
	name string
}

func main() {
	promise := async.NewPromise(func() (User, error) {
		time.Sleep(2 * time.Second)
		return User{name: "Test"}, nil
	})

	fmt.Println("do someting else")

	user, err := promise.Await(context.Background())
	if err != nil {
		log.Panic(err)
	}
	fmt.Println(user)
}
```

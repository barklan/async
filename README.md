# async go fork

**Uses [`golang.org/x/sync/errgroup`](https://pkg.go.dev/golang.org/x/sync/errgroup) internally. API is not changed.**

```go
import (
    "context"
    "github.com/barklan/async"
)

type MyData struct {/* ... */}

func AsyncFetchData(ctx context.Context, dataID int64) async.Promise[MyData] {
    return async.NewPromise(func() (MyData, error) {
        /* ... */
        return myDataFromRemoteServer, nil
    })
}

func DealWithData(ctx context.Context) {
    myDataPromise := AsyncFetchData(ctx, 451)
    // do other stuff while operation is not settled
    // once your ready to wait for data:
    myData, err := myDataPromise.Await(ctx)
    if err != nil {/* ... */}
}
```

## SDK

针对不同的版本，etcd提供了两个版本的sdk, 下面针对不同版本，来使用熟悉下。

#### v2

**Install**

```
go get go.etcd.io/etcd/client
```

**使用**

```
package main

import (
	"context"
	"fmt"
	"time"

	"go.etcd.io/etcd/client"
)

func main() {
	cfg := client.Config{
		Endpoints:               []string{"http://127.0.0.1:2379"},
		Transport:               client.DefaultTransport,
		HeaderTimeoutPerRequest: time.Second,
	}

	c, err := client.New(cfg)
	if err != nil {
		fmt.Println(err)
	}

	kapi := client.NewKeysAPI(c)

	// set /foo bar
	resp, err := kapi.Set(context.Background(), "/foo", "bar", nil)
	if err != nil {
		fmt.Println(err)
	}

	fmt.Println(resp)

	// get /foo
	resp, err = kapi.Get(context.Background(), "/foo", nil)
	if err != nil {
		fmt.Println(err)
	}

	fmt.Println(resp)
}
```

**异常处理**
etcd client 可能会返回以下几种类型的异常
- context error
- cluster error
- response error
   
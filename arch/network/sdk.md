## SDK

针对不同的版本，etcd提供了两个版本的sdk, 下面针对不同版本，来使用熟悉下。

### v2

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
每一个API调用的第一个参数都是context。 context可以被取消或者是检测其期限。如果context被取消了或者到了生命周期，
将会返回context异常。 
- cluster error
每一次API调用都会挨个发送请求到etcd集群，直到获得响应。 如果一个发送到etcd集群中某个节点的请求失败了，异常将会添加到异常列表里面， 如果整个集群中所有节点都失败了，则会返回一个集群异常。
- response error
如果从集群中获得的响应是无效的， 会返回响应异常。


#### 注意事项
 
1. 在节点正常工作的情况下，etcd/client优先会使用同一个集群节点。他会保存socket连接，提高客户端跟服务器之间的效率。 这个并不会影响数据的一致性， 因为复制到每个有效节点中的数据已经是一致的。


2. etcd/client 采用了round-robin的负载均衡策略来选择可用的节点进行交互。 例如，如果其中一个节点失效了，会转发到其他的节点。

3. 默认情况下etcd/client不能处理服务器端的SIGSTOPed, tcp keepalive机制在这种情况下是无用的，因为操作系统仍旧会发送tcp包。我们也有计划去提高这方面的功能，但就目前来说，优先级并不高，所以没必要刻意去关注。

4. etcd/client 不会检测成员健康状态。 如果成员从集群中分裂出来，etcd/client 会检索到过时的数据。故而，用户需要自己关注集群状态。


### V3
etcd/clientv3 是一个官方的V3版本的Go语言etcd客户端。

**安装**
```
go get go.etcd.io/etcd/clientv3
```

**使用**
```go
package main

import (
	"context"
	"fmt"
	"time"

	"go.etcd.io/etcd/clientv3"
)

func main() {
	cli, err := clientv3.New(clientv3.Config{
		Endpoints:   []string{"10.103.113.127:2379"},
		DialTimeout: 5 * time.Second,
	})

	if err != nil {
		fmt.Println(err)
	}
	defer cli.Close()

	var timeout time.Duration
	timeout = 5 * time.Second
	ctx, cancel := context.WithTimeout(context.Background(), timeout)

	resp, err := cli.Get(ctx, "magic")
	defer cancel()

	if err != nil {
		fmt.Println(err)
	}

	fmt.Println(resp)

	for {
		wrsp := cli.Watch(ctx, "magic")
		for rsp := range wrsp {
			fmt.Println(rsp)
			for _, ev := range rsp.Events {
				fmt.Println(ev)
				// fmt.Printf("%s %q : %q\n", ev.Type, ev.Kv.Key, ev.Kv.Value)
			}
		}
	}
}
```

**异常处理**
etcd/clientv3 会返回两种类型的异常：
- context error
- gRPC error
  






## 代理

etcd根据协议的不同， 提供了三种不同形式的代理。分别为：
- tcpproxy
- grpcproxy
- httpproxy

下面我们看一个使用tcpproxy的demo

```go
package main

import (
	"fmt"
	"net"
	"net/http"
	"net/http/httptest"
	"net/url"
	"go.etcd.io/etcd/proxy/tcpproxy"
)

func main() {
	l, err := net.Listen("tcp", "127.0.0.1:0")
	if err != nil {
		fmt.Println(err)
	}

	defer l.Close()

	want := "hello proxy"

	ts := httptest.NewServer(http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprint(w, want)
	}))

	defer ts.Close()

	u, err := url.Parse(ts.URL)

	fmt.Println(u)
	if err != nil {
		fmt.Println(err)
	}
	var port  uint16
	fmt.Sscanf(u.Port(), "%d", &port)


	p := tcpproxy.TCPProxy{
		Listener: l,
		Endpoints: []*net.SRV{{
			Target: u.Hostname(), Port: port,	
		}},
	}
	p.Run()
}
```

如此，客户端可以运行 `curl http://127.0.0.1:port` 查看。





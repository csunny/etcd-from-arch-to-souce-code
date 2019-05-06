## 命令行

etcdctl 是etcd集群的命令行工具。 我们可以在服务器或者是在脚本中通过etcdctl来进行集群的操作、管理和维护。

前面已经提到了，etcdctl也有两个版本，我们在使用过程中，需要注意版本对应关系。 首先我们来看看etcdctl v2的使用。

### V2
#### 配置
--debug 
-   输出curl命令，可以用来重现request请求

```
etcdctl --debug  get magic
------------
start to sync cluster using endpoints(http://127.0.0.1:4001,http://127.0.0.1:2379)
cURL Command: curl -X GET http://127.0.0.1:4001/v2/members
cURL Command: curl -X GET http://127.0.0.1:2379/v2/members
got endpoints(http://10.103.113.127:2379) after sync
Cluster-Endpoints: http://10.103.113.127:2379
cURL Command: curl -X GET http://10.103.113.127:2379/v2/keys/magic?quorum=false&recursive=false&sorted=false
22
```

--no-sync
-   在发送request请求之前不会同步集群信息
-   使用此选项可访问未发布的客户端
-   没有这个参数，--endpoint的值将被etcd集群覆盖

--output, -o
-   用指定的格式输出响应 （simple， extended或者json）
-   默认: simple

--discovery-srv, -D
-   domain name to query for SRV records describing cluster endpoints
-   默认： none
-   环境变量： ETCDCTL_DISCOVERY_SRV
  
--peers
-  逗号分割的集群地址列表
-  默认： http://127.0.0.1:2379
-  环境变量: ETCDCTL_PEERS

--endpoints
-  逗号分割的集群地址列表
-  默认：http://127.0.0.1:2379
-  环境变量：ETCDCTL_ENDPOINT
-  没有--no-sync 参数的时候，将会被etcd集群覆盖.

--cert-file
-  使用SSL认证的HTTPS客户端证书文件
-  默认值：none
-  环境变量： ETCDCTL_CERT_FILE

--key-file
-  使用SSL认证的HTTPS客户端key文件
-  默认： none
-  环境变量 ETCDCTL_KEY_FILE

--ca-file
-  ca证书认证
-  默认： none
-  环境变量： ETCDCTL_CA_FILE

--username, -u
- 用户名：密码认证
- 默认： none
- 环境变量： ETCDCTL_USERNAME

--timeout 
-  每次请求的连接超时时间
-  默认 1s

--total-timeout
- 命令异常超时时间
- 默认：5s


#### 使用案例

##### 设置key值
给/foo/bar 这个key设置一个值
```
etcdctl set /foo/bar  "Hello World"
Hello World
```

设置一个具有60s过期时间的key
```
etcdctl set /foo/bar "Hello World" --ttl 60
Hello World
```

带条件的设置, 当之前的值为"Hello World" 时，设置值为 "Goodbye world"

```
etcdctl set /foo/bar  "Goodbye world"  --swap-with-value "Hello world"
Goodbye world
```

带条件的设置，当/foo/bar在etcd中的索引为12时，设置对应key的值

```
etcdctl set /foo/bar  "Goodbye world" --swap-with-index 12
Goodbye world
```

当key不存在时，创建一个新key

```
etcdctl mk /foo/new_bar  "Hello world"
Hello world
```

按照次序常见一个新的key 在文件夹/fooDir下

```
etcdctl mk --in-order /fooDir  "Hello world"
```

当目录不存在时，创建一个新目录

```
etcdctl mkdir /fooDir
```

更新一个已存在的key /foo/bar

```
etcdctl update /foo/bar  "Hala mundo"
Hala mundo
```

创建或者更新一个叫/mydir 的目录

```
etcdctl setdir /mydir
```

##### 检索key
获取当前key的值

```
etcdctl get /foo/bar
Hello world
```

获取key的值以及一些额外的元数据信息

```
etcdctl -o extended get /foo/bar

Key: /foo/bar
Created-Index: 279
Modified-Index: 279
TTL: 0
Index: 280

Hello World
```

##### 列举目录

```
etcdctl ls

```

递归列举出所有的目录

```
etcdctl ls --recursive
```

##### 删除key

```
etcdctl rm  /foo/bar
```

删除一个空的目录或者键值对

```
etcdctl rmdir  /path/to/dir
or
etcdctl rm  /path/to/dir  --dir
```

递归删除key以及子key

```
etcdctl rm /foo/bar --recursive
```

带条件的删除

```
etcdctl rm /foo/bar  --with-value "Hello world"
```

##### Watch监听
监听key的下一个变化

```
etcdctl watch  /foo/bar
```

持续监听

```
etcdctl watch /foo/bar  --forever

Hello world

.... client hangs forever until ctrl+C  printing values as key change
```

##### 返回码

etcd会返回以下返回码

```
0     Success
1     Malformed etcdctl arguments
2     Failed to connect to host
3     Failed to auth   (client cert rejected, ca validation failure, etc)
4     400 error from etcd
5     500 error from etcd
```


##### Endpoint
可以通过endpoint进行远程连接etcd集群，进行相应的操作

```
etcdctl --endpoint http://10.0.28.1:4002 my-key to-a-value
etcdctl --endpoint http://10.0.28.1:4002,http://10.0.28.2:4002,http://10.0.28.3:4002 etcdctl set my-key to-a-value
```

##### 用户名和密码

如果etcd集群经过认证保护，可以通过指定用户名和密码的方式进行访问

```
ETCDCTL_USERNAME="root:password" etcdctl set my-key to-a-value
```

##### DNS 发现
为了通过SRV记录进行etcd的集群服务发现， 指定 --discovery-srv参数或者ETCDCTL_DISCOVERY_SRV 环境变量。 此操作优先级高于 --endpoint 参数

```
ETCDCTL_DISCOVERY_SRV="some-domain" etcdctl set my-key to-a-value
etcdctl --discovery-srv some-domain set my-key to-a-value
```


### V3



### 参考
- https://github.com/etcd-io/etcd/blob/master/etcdctl/README.md
- https://github.com/etcd-io/etcd/blob/master/etcdctl/READMEv2.md



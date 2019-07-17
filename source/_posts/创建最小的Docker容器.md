---
date: 2016-12-29 22:45:16
title: 创建最小的 Docker 容器
categories: docker
---

使用 Dockerfile 来创建一个空镜像

```
FROM scratch
```

使用 Go 编写一个简易的 Web 服务

``` go
// go-examples/basic/webserver
package main

import "net/http"
import "fmt"
import "log"

func index(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintln(w, "Hello World")
}

func main() {
	http.HandleFunc("/", index)
	err := http.ListenAndServe(":8000", nil)
	if err != nil {
		log.Println(err)
	}
}

```

使用 Go 语言的交叉编译，编译 Linux 环境的可执行文件

```bash
GOOS=linux GOARSH=amd64 go build
```

编辑 Dockerfile 文件，复制 Go 的可执行文件到镜像并在运行时运行

```dockerfile
FROM scratch
COPY ./webserver /
CMD ["./webserver"]
```

使用 Dockerfile 构建镜像

```bash
dokcer build -t goweb .
```

运行 goweb 镜像

```bash
docker run --name goserver -d -p 8080:8000 goweb
```

用浏览器访问 localhost:8080 就可以访问到 Web 服务，看到 Hello World

使用 `docker images` 可以看到 goweb 镜像的大小只有6M不到
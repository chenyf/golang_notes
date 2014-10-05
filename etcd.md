* time.Tick(duration)会创建一个Time类型的channel，用于实现定时器
```
Tick(d Duration) <-chan Time
```

* http.Serve()或者http.ListenAndServe()，可以通过实现http.Handler接口来实现自定义的WEB server
```
type Handler interface {
    ServeHTTP(ResponseWriter, *Request)
}
```

* json.NewEncoder()接受一个io.Writer参数，生成一个编码器
```
func NewEncoder(w io.Writer) *Encoder
```

* 在结构里面组合进一个接口的用法很常见
```
type CORSHandler struct {
    Handler http.Handler
	Info    *CORSInfo
}
```

* 在golang里面，接口用的非常多，要注意，下面是常见的接口
```
package builtin
type error interface {
	Error() string
}

package io
type Reader interface {
	Read(p []byte) (n int, err error)
}

type Writer interface {
	Write(p []byte) (n int, err error)
}

type Closer interface {
	Close() error
}

type ReadWriter interface {
	Reader
	Writer
}

package http
type Handler interface {
	ServeHTTP(ResponseWriter, *Request)
}
```

* 常用的golang package
** fmt
** log
** strings
** bytes
** time
** encoding/json
** bufio
** container
** errors
** flag
** io
** io.util
** os
** path
** sort
** regexp
** stringconv
**

* etcd里面的周期性
etcd通过 time.Tick()产生定时事件，
定时发生后，向raft node server的一个channel推送一个空结构体消息
raft node server通过select监听此channel，当有消息到达后，调用当前状态下的 tick函数，例如tickHeartbeat
这种select的使用方式，可以实现事件驱动的server逻辑，非常重要！


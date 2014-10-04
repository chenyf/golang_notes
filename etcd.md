
1. time.Tick(duration)会创建一个Time类型的channel，用于实现定时器
2. http.Serve()或者http.ListenAndServe()，可以通过实现http.Handler接口来实现自定义的WEB server
```
type Handler interface {
    ServeHTTP(ResponseWriter, *Request)
}
```
3. json.NewEncoder()接受一个io.Writer参数，生成一个编码器
```
func NewEncoder(w io.Writer) *Encoder
```
4. 在golang里面，接口用的非常多，要注意
5. 注意在结构里面组合一个接口的用法


# go context

context作用于多个goroutine做任务取消用

context.newxxx出来的都是子context, 父context取消, 其实就是关闭channel, 会把所有的子context都取消

ctx, cancel := context.WithCancel(context.Background())

任意地方可以调用cancel来取消这个context, 在对应的goroutine里面需要监听ctx.Done chan, 最后通过ctx.Err()来获得错误原因, 其实就是cancel或者deanline设置的

# containerd 例子

containerd里面cri接口, 导出都是context, 最后会传递到干活的地方, 比如http请求, 根据ctx.Done来判断这个context是否为取消

```
func Do(ctx context.Context, client *http.Client, req *http.Request) (*http.Response, error) {
	resp, err := client.Do(req.WithContext(ctx))
	if err != nil {
		select {
		case <-ctx.Done():
			err = ctx.Err()
		default:
		}
	}
}
```

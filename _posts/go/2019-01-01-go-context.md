# go context

context作用于多个goroutine做任务取消用

context.newxxx出来的都是子context, 父context取消, 会把所有的子context都取消

ctx, cancel := context.WithCancel(context.Background())

任意地方可以调用cancel来取消这个context, 在对应的goroutine里面需要监听ctx.Done chan, 最后通过ctx.Err()来获得错误原因, 其实就是cancel或者deanline设置的
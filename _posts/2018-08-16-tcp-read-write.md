# tcp的读写调用原理

几个重要的结论：

1. read总是在接收缓冲区有数据时立即返回，而不是等到给定的read buffer填满时返回。

只有当receive buffer为空时，blocking模式才会等待，而nonblock模式下会立即返回-1（errno = EAGAIN或EWOULDBLOCK）

2. blocking的write只有在缓冲区足以放下整个buffer时才返回（与blocking read并不相同）

nonblock write则是返回能够放下的字节数，之后调用则返回-1（errno = EAGAIN或EWOULDBLOCK）


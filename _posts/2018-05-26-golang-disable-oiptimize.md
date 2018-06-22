# golang去优化

makefile去优化挺麻烦的, 改个编译器简单

一个是go命令, 一个是compile命令, go调用compile, 但是不会传递环境变量过去, 这样最简单

```
diff --git a/src/cmd/compile/internal/gc/main.go b/src/cmd/compile/internal/gc/main.go
index b651c9a..3ec36e5 100644
--- a/src/cmd/compile/internal/gc/main.go
+++ b/src/cmd/compile/internal/gc/main.go
@@ -239,6 +239,10 @@ func Main(archInit func(*Arch)) {
        flag.StringVar(&benchfile, "bench", "", "append benchmark times to `file`")
        objabi.Flagparse(usage)

+       if !compiling_runtime {
+               Debug['N'] = 1
+               Debug['l'] = 1
+       }
        // Record flags that affect the build result. (And don't
        // record flags that don't, since that would cause spurious
        // changes in the binary.)
```

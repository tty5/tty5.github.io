# golang去优化

makefile去优化挺麻烦的, 改个编译器简单

```
diff --git a/src/cmd/compile/internal/gc/main.go b/src/cmd/compile/internal/gc/main.go
index b651c9a..22e0334 100644
--- a/src/cmd/compile/internal/gc/main.go
+++ b/src/cmd/compile/internal/gc/main.go
@@ -239,6 +239,11 @@ func Main(archInit func(*Arch)) {
        flag.StringVar(&benchfile, "bench", "", "append benchmark times to `file`")
        objabi.Flagparse(usage)

+       if !compiling_runtime && os.Getenv("fuck") == "x"{
+               Debug['N'] = 1
+               Debug['l'] = 1
+       }
+
        // Record flags that affect the build result. (And don't
        // record flags that don't, since that would cause spurious
        // changes in the binary.)
diff --git a/src/cmd/go/main.go b/src/cmd/go/main.go
index 497970b..176bff6 100644
--- a/src/cmd/go/main.go
+++ b/src/cmd/go/main.go
@@ -78,6 +78,15 @@ func main() {
                base.Usage()
        }

+       if os.Getenv("fuck") == "x" {
+               if len(args) >= 2 && args[0] == "build" {
+                       tmp := args[ len(args) - 1 ]
+                       args[ len(args) - 1 ] = "-gcflags"
+                       args = append(args, "-N -l")
+                       args = append(args, tmp)
+               }
+       }
+
        cfg.CmdName = args[0] // for error messages
        if args[0] == "help" {
                help.Help(args[1:])
```

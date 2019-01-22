# bash esc
bash esc hex是0x1b, 很多控制字符含义, 都是它开头

比如颜色
```
\033就是ox1b
RED='\033[0;31m'
NC='\033[0m' # No Color
printf "I ${RED}love${NC} Stack Overflow\n"
```

比如ctrl left ctrl right
```
bind '"\e[1;5D" backward-word' 
bind '"\e[1;5C" forward-word'
```

都是输入了esc开头的字节流

# bash set 功能列表
```
set -u就用来改变这种行为。脚本在头部加上它，遇到不存在的变量就会报错，并停止执行
set -x用来在运行结果之前，先输出执行的那一行命令
set -e从根本上解决了这个问题，它使得脚本只要发生错误，就终止执行

Bash 会把最后一个子命令的返回值，作为整个命令的返回值
set -o pipefail用来解决这种情况，只要一个子命令失败，整个管道命令就失败，脚本就会终止执行
```

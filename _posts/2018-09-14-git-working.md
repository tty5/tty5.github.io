# git各个工作区操作

## work区操作

#### work区自己改
自己改就自己改

#### work区某个文件同步为stage里面的内容
git co -- file

git co不加版本号就是从stage签出

#### work区某个文件同步为repo里面的内容

git co HEAD -- file

加版本号就是同步repo的内容, stage, work都会变, git是从上到下的变, 不能跳着变

# git tips

## git pull github pr
git fetch origin pull/1/head

## git fetch
```git fetch url fetch```默认的refs

```git fetch url refs```把某个refs拿出来

```git fetch url refs/*:refs/tmp/*```一堆都拿出来


```
proxychains4 -q git fetch url refs/pull/4/head
proxychains4 -q git fetch url refs/pull/412/*:refs/tmp/*
```

## git co
```
git co -- file
```
git co 后面跟文件的时候, 表示把某个文件或者文件夹签出, 比如git co HEAD^^^ a.c stage区和work区都会更改, 如果不加版本号, 就从stage签出

git co 如果没有跟文件名, 那么就是把版本区, stage区, work区都签过去, **改变work区的时候, 如果和本地修改文件没有冲突, 就直接过去了**

## git reset
```
git reset -- file
```
git reset 有文件, 就是把stage的某个文件变成版本文件, 可以理解为把stage的内容清掉, 没加版本就是HEAD

git reset 没有文件就是把整个stage变成某个版本, 没写版本就是HEAD


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

## stage区操作

#### 把stage区内容改成work区内容
git add

#### 把stage区内容改成repo内容
git reset -- file

## repo区操作

git reset --soft version 只修改repo区

#### 修改历史git version

git rebase -i 之前的版本, 然后edit, 然后修改git commit

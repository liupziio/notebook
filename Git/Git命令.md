##### 查看隐藏的git文件

```nginx
ls -ah
```



##### 查看文件修没修改的状态

```nginx
git status 文件
```



##### 查看文件上一次修改了什么

```nginx
git diff 文件
```



##### 丢弃工作区上一次文件的修改

```js
git checkout -- readme.txt
```



##### 提交文件

```nginx
git add 文件
git commit -m "add distributed"
```



##### 查看修改日志

+ 从最新修改到最早修改排序

```nginx
git log
```

+ 查看简约版日志

```nginx
git log --pretty=oneline
```



# 一、时光穿梭机



## 1、返回到某一个文件版本

1. 在git中``HEAD``表示当前版本，上一个版本是``HEAD^``，上上一个版本是``HEAD^^``，往上100个版本是``HEAD~100``



返回上一个版本

```nginx
git reset --hard HEAD^
```



2. 回到刚才的版本

可以根据以前的git log 出来的 commit 来返回到刚才替换的版本

例如是：6af61215b95f2c32c10fb0d3b1c6214d2e7c5bf4

```nginx
git reset --hard 6af6
```



3. 如果关机了，也可以通过 ``git reflog``命令来找到
   + ``git reflog``命令可以记录每一次的操作

```nginx
$ git reflog

6af6121 (HEAD -> master) HEAD@{0}: reset: moving to 6af6
21a429d HEAD@{1}: reset: moving to HEAD^
6af6121 (HEAD -> master) HEAD@{2}: commit: append GPL
21a429d HEAD@{3}: commit: append GPL
90c5f74 HEAD@{4}: commit (initial): add distributed

```



## 2、工作区与暂存区





+ stage是暂存区
+ master是分支



+ 添加

```nginx
#个别添加
git add readme.txt
git add LICENSE
#全部添加
git add . 
```





![git-stage](https://www.liaoxuefeng.com/files/attachments/919020074026336/0)



+ 将暂存区的全都提交给分支

```nginx
#""里边的是大意是远程仓库在每一个文件后边简单说明，可自己改，
git commit -m "understand how stage works"
```



![git-stage-after-commit](https://www.liaoxuefeng.com/files/attachments/919020100829536/0)



## 3、撤销删除

1.没有`git add`时，用`git checkout -- file`

2.已经`git add`时，先`git reset HEAD <file>`回退到1.，再按1.操作

3.已经`git commit`时，用`git reset --hard HEAD^`回退上一个版本



# 二、远程仓库



## 1、远程仓库与本地仓库链接

1. GitHub上创建一个新的仓库
   + 名叫做 learngit



2. Github仓库与本地仓库关联

```nginx
$ git remote add origin git@github.com:liupziio/learngit.git
```



3. 本地仓库内容推送给远程仓库
   + 由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

```nginx
$ git push -u origin master
```

+ 这时远程库刷新就和本地仓库一样了



4. 之后再修改提交时就可以通过命令

```js
$ git push origin master
```

+ 把本地`master`分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！



## 2、把远程库克隆到本地



1. 创建一个名为`gitskills`的仓库
   + 并且勾选`Initialize this repository with a README`
     + 勾选之后创建一个叫`README.md`的自述文件
   + 创建成功之后

```nginx
$ git clone git@github.com:liupziio/gitskills.git
```



2. 查看克隆到本地的库

```nginx
$ cd gitskills
$ ls
README.md
```



## 3、本地传到远程库

1. 添加到本地

```js
#个别添加
git add readme.txt
git add LICENSE
#全部添加
git add . 
```



2. 将暂存区的提交到本地分支

```js
#""里边的是大意是远程仓库在每一个文件后边简单说明，可自己改，
git commit -m "666"
```



3. 将分支中的数据提交到远程仓库

```js
#将分支中所有data提交到远程仓库
git push 
```







# 三、分支管理



## 1、分支的查看，创建，切换，合并，删除



1. 创建并且切换到分支dev

```nginx
git switch -c dev
```

+ 创建分支
  + git switch <name>
+ 切换分支
  + git switch <name>



2. 查看所有分支和当前分支

```nginx
$ git branch
* dev	前边带*的是当前分支
  master
```



3. 合并分支

   + 在当前分支下创建一个readme.txt文件

   + 之后提交

     + ```nginx
       $ git add readme.txt 
       ```

```nginx
$ git merge dev
#将dev分支合并到当前分支
Updating d46f35e..b17d20e
Fast-forward
 readme.txt | 1 +
 1 file changed, 1 insertion(+)
```

+ `git merge`命令用于合并指定分支到当前分支。合并后，再查看`readme.txt`的内容，就可以看到，和`dev`分支的最新提交是完全一样的。



4. 删除分支

```nginx
$git branch -d <name>
```



## 2、推送分支

1. 查看远程库信息

```nginx
$ git remote -v
```

+ 上面显示了可以抓取和推送的`origin`的地址。如果没有推送权限，就看不到push的地址。



2. 推送分支
   + 推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：

```nginx
$ git push origin master
#把本地master推送到远程的push
```



如果要推送其他分支，比如`dev`，就改成：

```nginx
$ git push origin dev
#把本地dev推送到远程的push
```



- `master`分支是主分支，因此要时刻与远程同步；
- `dev`分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
- bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
- feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。



### 小结



- 查看远程库信息，使用`git remote -v`；
- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
- 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
- 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。



# 四、标签管理



## 1、创建标签

- 命令`git tag <tagname>`用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；
- 命令`git tag -a <tagname> -m "blablabla..."`可以指定标签信息；
- 命令`git tag`可以查看所有标签。



## 2、操作标签

- 命令`git push origin <tagname>`可以推送一个本地标签；
- 命令`git push origin --tags`可以推送全部未推送过的本地标签；
- 命令`git tag -d <tagname>`可以删除一个本地标签；
- 命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。
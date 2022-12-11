安装完成后，还需要最后一步设置，在命令行输入：

`$ git config --global user.name "Your Name"` 这里的名字最好和 **github** 的账户名相同
`$ git config --global user.email "email@example.com"`
注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

创建版本库
建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录：

~~~
$ mkdir learngit
$ cd learngit
$ pwd
~~~

/Users/michael/learngit
pwd命令用于显示当前目录
第二步，通过git init命令把这个目录变成Git可以管理的仓库：
`$ git init`
Initialized empty Git repository in /Users/michael/learngit/.git/
瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。

如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用ls -ah命令就可以看见。
言归正传，现在我们编写一个readme.txt文件，内容如下：

Git is a version control system.
Git is free software.
一定要放到learngit目录下（子目录也行）
第一步，用命令git add告诉Git，把文件添加到仓库：

$ git add readme.txt

第二步，用命令git commit告诉Git，把文件提交到仓库：

$ git commit -m "wrote a readme file"
[master (root-commit) eaadf4e] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
简单解释一下git commit命令，-m后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。
git commit命令执行成功后会告诉你，1 file changed：1个文件被改动（我们新添加的readme.txt文件）；2 insertions：插入了两行内容（readme.txt有两行内容）。

为什么Git添加文件需要add，commit一共两步呢？因为commit可以一次提交很多文件，所以你可以多次add不同的文件，比如：
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."



## 添加远程库

### 本地有 Git 仓库，并且我们已经进行了多次`commit`操作 

`$ git init`

登陆GitHub，创建一个新的仓库，也不用创建readme。

目前，在GitHub上的这个`learngit`仓库还是空的 

目前，在GitHub上的这个`learngit`仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。

[![提示1](https://s1.ax1x.com/2022/12/10/zWIT4P.png)](https://imgse.com/i/zWIT4P)

[![提示2](https://s1.ax1x.com/2022/12/09/zWGk34.png)](https://imgse.com/i/zWGk34)

现在，我们根据GitHub的提示，在本地的`learngit`仓库下运行命令：

`$ git remote add origin https://github.com/RicardoSJin/learngit.git `

添加后，远程库的名字就是`origin`，这是Git默认的叫法，也可以改成别的，但是`origin`这个名字一看就知道是远程库。 

再用以下指令创建一个新的分支

`$ git branch -M main`

下一步，就可以把本地库的所有内容推送到远程库上

`$ git push -u origin master` 或 `$ git push -u origin master`

由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。 

从现在起，只要本地作了提交，就可以通过命令：

```
$ git push origin master
```

### 本地没有 Git 仓库，这时我们可以直接将远程仓库`clone`到本地 

首先，建立一个本地仓库 

进入该仓库，进入`init`初始化操作 

用命令`$ git clone origin https://github.com/~ ` 关联远程仓库

### 删除远程库

如果添加的时候地址写错了，或者就是想删除远程库，可以用`git remote rm <name>`命令。使用前，建议先用`git remote -v`查看远程库信息：

```
$ git remote -v
origin  git@github.com:michaelliao/learn-git.git (fetch)
origin  git@github.com:michaelliao/learn-git.git (push)
```

然后，根据名字删除，比如删除`origin`：

```
$ git remote rm origin
```

此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。

## Git 进阶之「设置别名」

`git config --global alias.co check`

如上所示，这样我们就设置`checkout`的别名为`co`啦！也就是说，以后我们直接输入`git co`，就表示`git checkout`啦，特别是对于一些组合操作，例如： 

- `git config --global alias.psm 'push origin master'`
- `git config --global alias.plm 'pull origin master`

实用命令：

1.   

~~~
git log --graph --pretty=format:'%Cred%h%Creset - %C(yellow)%d%Creset %s %Cgreen(%cr) 
%C(bold blue)<%an>%Creset' --abbrev-commit --date=relative
~~~

日志看着更加清楚啦！ 



2.  

   `$ git config -l `

   可以查看本机 Git 配置的命令，可以展示`color.ui`、`core.repositoryformatversion`和`core.filemode`等配置信息。

## 回滚 Git 提交到 GitHub 的 commit 记录

 首先，找到想要回退到某个版本的版本号 

查看版本号的命令用`git log` 

[![查看版本号](https://s1.ax1x.com/2022/12/10/zWvawT.png)](https://imgse.com/i/zWvawT)

`git reset --hard <版本号>`或者`git reset --soft <版本号>`

对于上述两条命令，仅有`--hard`和`--soft`参数的不同，两者的区别是：

`--hard`，抛弃当前工作区的修改
`--soft`，回退到之前的版本，但保留当前工作区的修改，可以重新提交
执行完本地回滚之后，还需要执行如下命令，同步远端的内容：

`git push origin <分支名>`
在执行上述命令的时候，可能会提示本地的版本落后于远端的版本，因此我们还需要在上述命令中加上--force参数：

`git push origin <分支名> --force`

## 详述 Git 的 rebase 命令使用方法

[CSDN链接][(2条消息) 详述 Git 的 rebase 命令使用方法_CG国斌的博客-CSDN博客_git rebase命令](https://blog.csdn.net/qq_35246620/article/details/124718643) 



## 创建与合并分支

在[版本回退](https://www.liaoxuefeng.com/wiki/896043488029600/897013573512192)里，你已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即`master`分支。`HEAD`严格来说不是指向提交，而是指向`master`，`master`才是指向提交的，所以，`HEAD`指向的就是当前分支。

一开始的时候，`master`分支是一条线，Git用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点：

![](https://www.liaoxuefeng.com/files/attachments/919022325462368/0)

每次提交，`master`分支都会向前移动一步，这样，随着你不断提交，`master`分支的线也越来越长。

当我们创建新的分支，例如`dev`时，Git新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上：

![git-br-create](https://www.liaoxuefeng.com/files/attachments/919022363210080/l)

不过，从现在开始，对工作区的修改和提交就是针对`dev`分支了，比如新提交一次后，`dev`指针往前移动一步，而`master`指针不变：

![git-br-dev-fd](https://www.liaoxuefeng.com/files/attachments/919022387118368/l)

假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上。Git怎么合并呢？最简单的方法，就是直接把`master`指向`dev`的当前提交，就完成了合并：

![git-br-ff-merge](https://www.liaoxuefeng.com/files/attachments/919022412005504/0)

合并完分支后，甚至可以删除`dev`分支。删除`dev`分支就是把`dev`指针给删掉，删掉后，我们就剩下了一条`master`分支：

![git-br-rm](https://www.liaoxuefeng.com/files/attachments/919022479428512/0)



### 实战

首先，我们创建并切换到`dev`分支，修改并提交

`dev`分支的工作完成，我们就可以切换回`master`分支 

切换回`master`分支后，再查看一个`readme.txt`文件，刚才添加的内容不见了！因为那个提交是在`dev`分支上，而`master`分支此刻的提交点并没有变：

![git-br-on-master](https://www.liaoxuefeng.com/files/attachments/919022533080576/0)



现在，我们把`dev`分支的工作成果合并到`master`分支上：

~~~
$ git merge dev
Updating 5c86b41..b75b50b
Fast-forward
 readme.txt | 3 ++-
 1 file changed, 2 insertions(+), 1 deletion(-)
~~~

注意到上面的`Fast-forward`信息，Git告诉我们，这次合并是“快进模式”，也就是直接把`master`指向`dev`的当前提交，所以合并速度非常快。 

合并完成后，就可以放心地删除`dev`分支了 

~~~
$ git branch -d dev
~~~

### Git鼓励大量使用分支：

查看分支：`git branch`

创建分支：`git branch <name>`

切换分支：`git checkout <name>`或者`git switch <name>`

 `$ git checkout -b <name>`加上`-b`参数表示创建并切换 

创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`

合并某分支到当前分支：`git merge <name>`

删除分支：`git branch -d <name>`
# Git教程 
# Git是目前世界上最先进的分布式版本控制系统（没有之一）
# 安装Git
> 安装完成后，还需要最后一步设置，在命令行输入：
```    
git config --global user.name "Your Name"          
git config --global user.email "email@example.com" 
```
> 注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置        

# 创建版本库    
> 版本库又名仓库，英文名repository，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，      
> 每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”.        

* 首先，选择一个合适的地方，创建一个空目录
``` 
mkdir someDir
cd someDir
```      
* 第二步，通过`git init`命令把这个目录变成Git可以管理的仓库    
```    
git init    
```   
瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository）,这个目录是Git来跟踪管理版本库的，     
没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了      

## 小结           
- 初始化一个Git仓库，使用`git init`命令。             
- 添加文件到Git仓库，分两步           
> - 第一步，使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；          
> - 第二步，使用命令`git commit`，完成。         

# 把文件添加到版本库    
比如我们在刚刚创建的`someDir`中编写一个`readme.md`文件     
* 第一步，用命令`git add`告诉Git，把文件添加到仓库
```   
git add readme.md    
```
* 第二步，用命令`git commit`告诉Git，把文件提交到仓库    
```
git commit -m "wrote a readme file"    
```
简单解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，      
这样你就能从历史记录里方便地找到改动记录。         

为什么Git添加文件需要add，commit一共两步呢？因为commit可以一次提交很多文件，所以你可以多次add不同的文件，比如：
```
git add file1.txt
git add file2.txt file3.txt
git commit -m "add 3 file"    
```
* 当我们修改```readme.md```后，运行git status命令看看结果     
```
On branch master
Your branch is up-to-date with 'origin/master'.
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README.md

(use "git add <file>..." to include in what will be committed) 
```
`git status`命令可以让我们时刻掌握仓库当前的状态，上面的命令告诉我们，readme.md被修改过了，但还没有准备提交的修改    

如果能看看具体修改了什么内容,需要用git diff这个命令看看  

## 小结    
- 要随时掌握工作区的状态，使用`git status`命令        
- 如果git status告诉你有文件被修改过，用`git diff`可以查看修改内容      

# 版本回退     
每当你觉得文件修改到一定程度的时候，就可以“保存一个快照”，这个快照在Git中被称为commit。      
一旦你把文件改乱了，或者误删了文件，还可以从最近的一个commit恢复，然后继续工作，而不是把几个月的工作成果全部丢失    
* 在Git中，我们用`git log`命令查看历史记录    
> git log命令显示从最近到最远的提交日志,如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数
> 一大串类似`3628164...882e1e0`的是`commit id`（版本号），和SVN不一样，Git的`commit id`不是1，2，3……递增的数字，    
> 而是一个SHA1计算出来的一个非常大的数字，用十六进制表示      

* 在Git中，用`HEAD`表示当前版本，也就是最新的提交的版本，上一个版本就是`HEAD^`，上上一个版本就是`HEAD^^`，      
当然往上100个版本写100个^不容易数不过来，所以写成`HEAD~100`        

* 当我们要回退到上一个版本时，可以使用`git reset`命令     
```
git reset --hard HEAD^
```
此时键入`git log`后，最新的版本已经不在了，如何恢复呢？
> 如果最新的版本的`commit id`是3628164...，于是就可以恢复回来   
```
git reset --hard 3628164
```
如果关掉了终端，此时最新版本的`commit id`就找不到了，怎么办？
> Git提供了一个命令`git reflog`用来记录你的每一次命令    
```
git reflog
```

## 小结    
- HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit id`         
- 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本        
- 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本    

# 工作区和暂存区   
* 工作区  
> 就是你在电脑里能看到的目录，比如`someDir`文件夹就是一个工作区    

* 版本库   
> 工作区有一个隐藏目录`.git`，这个不算工作区，而是Git的版本库     
Git的版本库里存了很多东西，其中最重要的就是称为`stage`（或者叫index）的暂存区,还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`     
> 用`git add`把文件添加进去，实际上就是把文件修改添加到**暂存区**      
> 用`git commit`提交更改，实际上就是把暂存区的所有内容提交到**当前分支**         

可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改      

# 管理修改    
为什么Git比其他版本控制系统设计得优秀，因为Git跟踪并管理的是修改，而非文件     
> 第一次修改 -> `git add` -> 第二次修改 -> `git commit`    
当你用`git add`命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，`git commit`只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交        
提交后，用`git diff HEAD -- readme.md`命令可以查看工作区和版本库里面最新版本的区别
为了保存提交第二次修改，可以这么做      
> 第一次修改 -> `git add` -> 第二次修改 -> `git add` -> `git commit`     

# 撤销修改    
* 在Git中，`git checkout -- file`可以丢弃工作区的修改     
命令`git checkout -- readme.md`意思就是，把`readme.md`文件在工作区的修改全部撤销，这里有两种情况
> - 一种是`readme.md`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态       
> - 一种是`readme.md`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态    

* 在Git中，命令`git reset HEAD file`可以把暂存区的修改撤销掉（unstage），重新放回工作区      

## 小结   
* 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`     
* 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD file`，就回到了场景1，第二步按场景1操作      
* 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考**版本回退**一节，不过前提是没有推送到远程库     

# 删除文件   
* 从版本库中删除该文件，那就用命令`git rm`删掉，并且`git commit`，同时删除工作区文件    
* 如果工作区文件被误删，用命令`git checkout -- file`把误删的文件恢复到最新版本     
`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”        

## 小结   
命令`git rm`用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。 




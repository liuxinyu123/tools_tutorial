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
- HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`         
- 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本        
- 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本    



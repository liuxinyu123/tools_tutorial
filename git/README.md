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


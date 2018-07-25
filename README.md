# LearnGit（上）

#### 文档介绍
    git教程


#### 安装教程

1.**git install**

> https://git-scm.com/downloads

2.**git config**

>  $ git config --global user.name "Your Name"

> $ git config --global user.email "email@example.com"

3.详细git教程

> https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013743256916071d599b3aed534aaab22a0db6c4e07fd0000
#### 基础操作

1.**git init**

    <pre>
    mkdir learngit//创建learngit文件夹（repository，仓库）
    cd learngit
    pwd //  ../learngit
    git init//创建版本库并初始化
</pre>

2.**git add <file>**
> 将文件加到仓库中
 
3.**git commit -m \<message>**
> 将文件提交到仓库中，并添加修改记录

4.**git status**
> 实时掌握工作区状态，

5.**git diff**
> 使用前可用git diff 查看版本差异（查看修改内容）

6.**git log**
> 查看由最近到最远的提交日志；(查看历史)
> 
> 加上--pretty=oneline可缩减输出信息。

####版本回退
在git中，用<font color=#0099ff>**HEAD表示当前版本即最新提交的版本**</font>，上个版本为HEAD^,上上个版本为HEAD^^,当然往上100个版本为HEAD~100.

1.**git reset --hard HEAD^**
> 将当前版本A回退到上一个版本B

2.**git reset --hard \<当前版本号A 的commit id 前几位>**
> 若在1中退回上个版本B后想追回当前版本A，指定A版本的commit id 的前几位就可以追回。
> 
> PS：当前git未关闭情况下可使用此方法追回

3.**若电脑关闭，重新打开时**无法查看git log
> 可采用**git reflog** 记录每一次命令(可返回未来版本),即可查看命令历史，以便要回到未来的版本

 ![](https://i.imgur.com/cKNvkUa.png)
####工作区和暂存区

lgit文件夹就是一个工作区（Working Directory） 

 .git（隐藏目录即版本库：Repository）

> git的版本库存了很多东西，其中最重要的就是stage（或者index）的暂存区，还要git为我们自动创建的第一个分支<font color=#d56073>**master**</font>,以及指向<font color=#d56073>**master**</font>的一个指针<font color=#d56073>**HEAD**</font>;

 ![](https://i.imgur.com/zN89DF7.png)


>**前文讲到的git add指的是将文件添加到<font color=#d56073>暂存区（index/stage）</font>中，
然后通过git commit提交更改，实际上是将暂存区中的所有内容提交到当前分支(此处为master).**

> 由于第一次创建git版本库时，git自动为我们创建了唯一一个分支master,所以现在git commit就是往master分支上提交更改。    

#### 管理修改
git的优点：

> git跟踪并管理的是修改，而非文件。
> 
即每次修改后，需要先git add（添加到暂存区），再git commit才能提交到分支中，且可以多次 add 一次性提交多个修改。（可用git diff查看版本之间的不同（未git commit前使用）） 

![](https://i.imgur.com/KjDhFfH.png)

####撤回修改
当文件修改后，需要撤回修改时，可用```git checkout -- <filename>```
> git checkout 可将文件恢复至上一个版本的状态：

> 1、自修改后未add到暂存区，则撤销修改至和版本库一模一样的状态。

> 2、修改后add 到暂存区后，又做修改，则撤销至和暂存区一模一样的状态。

> 总之git checkout -- \<filename>可以让文件回到最近一次git commit 或git add的状态。(**注：-- 必须有，否则将变为切换至另一分支的命令**)

![](https://i.imgur.com/0p6T8ge.png)

当修改后的文件并**add到暂存区时，**可用git reset HEAD \<filename>将暂存区的修改撤销掉（unstage），重新放回工作区。

>**1.git reset HEAD \<filename>**
    
将在暂存区的修改撤销至工作区

>2**.git checkout -- \<filename>**

再通过git checkout 将工作区的修改撤销至前一个版本。

> git reset
>  
> 既可以退回版本，又可以将暂存区的修改退回到工作区。当使用HEAD时，表示最新版本。


####删除文件

在git中，删除也是一个修改操作。

删除了文件test.txt：

**删除**

> 从版本库中删除，即git rm -- \<filename> ，若提交到分支中，需要git commit一下，则文件就从版本库中删除了。

**恢复**
> 该情形是误删除了某文件，但在版本库中仍存在，所以可以使用上节git checkout -- \<filename> 将误删除文件恢复到最新版本。

----------

**注：命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。**

----------

####远程仓库
1、在本地也可以创建多个仓库（在不同目录下即可）

2、在GitHub上创建自己的仓库
> 
（1）创建自己的GitHub账号
> 
（2）创建SSH key 
    
     在命令行下执行：
     ssh-keygen -t rsa -C "youremail@example.com"
     会产生“id_rsa（私钥）和id_rsa.pub（公钥）”两个文件密钥对。
（3）登陆GitHub，打开“AccountSetting”->“Add SSH Key”

    填写任意title，并在key文本框中粘贴id_rsa.pub文件的内容。
PS：GitHub中的仓库是public的，所以注意操作。




####分支管理
**1、创建并合并分支**

创建分支dev并切换到dev
> git checkout -b dev

查看当前所有分支，且当前分支前面会标一个*号
> git branch 


**在dev分支上修改master分支下的文件并add和commit（即在master分支下的文件基础上修改）**

切换到master分支

> git checkout master

合并dev分支到master  即覆盖master分支上的文件。

> git merge dev 

删除分支dev：

> git branch -d dev


**2、解决冲突**

**3、分支管理策略**

**4、Bug分支**

**5、Feature分支**

**6、多人协作**

**7、Rebase**

####标签管理
1、创建标签

2、操作标签
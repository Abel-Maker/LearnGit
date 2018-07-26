# LearnGit

#### 文档介绍
    git教程
#### 基础概念
> 
**<font size=3>Remote</font>:**远程主仓库
> 
**<font size=3>Repository</font>:**本地仓库
>
**<font size=3>Index</font>:**Git追踪树，暂存区
>
**<font size=3>workspace</font>:**本地工作区（即你编辑器的代码）

 ![](https://i.imgur.com/nVwJy5X.png)


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
**1、在本地也可以创建多个仓库（在不同目录下即可）**

**2、在GitHub上创建自己的仓库**
> 
（1）创建自己的GitHub账号
> 
（2）创建SSH key 
    


>      在命令行下执行：
     ssh-keygen -t rsa -C "youremail@example.com"
     会产生“id_rsa（私钥）和id_rsa.pub（公钥）”两个文件密钥对。
> 
（3）登陆GitHub，打开“AccountSetting”->“Add SSH Key”

>     填写任意title，并在key文本框中粘贴id_rsa.pub文件的内容。
> 
PS：GitHub中的仓库是public的，所以注意操作。

**3、添加远程库**

> （1）首先在GitHub上Create a new repo，如起名为learngit，完成这步则在GitHub上创建了一个名为learngit的空仓库。
> 
> （2）在本地仓库下运行命令：（关联远程库）
> 
>     git remote add origin git@github.com:***/learngit.git
>     注：***为你GitHub的账户名。（远程库的名字为origin）
> （3）将本地库内容推送（push）到远程库中
> 
>     git push -u origin master //第一次推送加上-u
>     
推送成功 ：
> 
   ![](https://i.imgur.com/IKIgy81.png)  
（4）之后再提交只需
> 
      git push origin master//即可
PS：
> 
   现在你已经拥有自己的分布式版本库。
第一次和github进行ssh连接时会有一个warning，yes回车即可。

4、克隆（clone）

> （1）在GitHub上创建一个测试库，并获取地址（或者已经有了远程库地址），            
>   如git@github.com:Abel-Maker/gitskills.git

> （2）克隆：
> 
>      git clone git@github.com:Abel-Maker/gitskills.git 
**success:**

![](https://i.imgur.com/rDbg4Ti.png)
>     
####分支管理
**1、创建并合并分支**

创建分支dev并切换到dev
> git branch dev //创建dev

> git checkout dev//切换到dev
> 
> git checkout -b dev//二合一命令：创建并切换到分支dev

查看当前所有分支，且当前分支前面会标一个*号
> git branch 


**在dev分支上修改master分支下的文件并<font color=#0000f>add和commit</font>（即在master分支下的文件基础上修改）**

切换到master分支

> git checkout master

合并dev分支到master  即覆盖master分支上的文件。

> git merge dev //合并前请确认dev 是在**master的基础上**修改的

删除分支dev：

> git branch -d dev


**2、解决冲突**


分支dev与master分支上的同一文件，存在不同的修改，且都已经提交，故存在冲突。
所以我们需要解决冲突。

（1）找到冲突
> git status
> 
![](https://i.imgur.com/7dxfGoB.png)
>
>发现test.php文件在两个分支中均存在修改。故进行第二步：

（2）查看文件
> cat test.php
> 
> ![](https://i.imgur.com/exlVJEw.png)
> 
Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，我们修改后保存,并再次git add 和git commit

（3）查看合并情况：
> git log --graph //查看所有合并情况
> 
>![](https://i.imgur.com/oorHz75.png)
>
> git log --graph --pretty=oneline --abbrev-commit//查看当前合并情况
> ![](https://i.imgur.com/9xxb1p9.png)
>
<font color=#00fff size=5>All in ALL:</font><font size=3>当git无法自动合并时，就必须解决冲突，解决冲突就是手动编辑有冲突的文件，并再提交，则合并成功。</font>

**3、分支管理策略**

分支适合团队分工合作时进行使用，每个人都以master为基础如1.0,每次新的功能开发再进行迭代，进行分支合并，

    PS：分支合并的基础是在master的基础（如文件的增加、文件内容的增加）之上合并，
        只能是master没有的地方修改，否则存在冲突。故这里要求master的稳定性！否则将产生冲突。
合并时不推荐采用fast forword，推荐如下：
<font color=000ff >```git merge --no-ff -m <message description> <branch>```</font>

**4、Bug分支**

在开发的过程中，经常会出现bug，故可以创建一个bug分支，进行修复bug，修复后可以合并分支，然后删除bug分支。

(1)新建bug分支bug-101：
> git checkout -b bug-101

(2)修复bug后提交：
> git add <filename>
> 
> git commit -m  "fix bug-101"

(3)切换到master分支：
> git checkout master

(4)合并分支bug分支
> git merge --no-ff -m "merge bug fix bug-101" bug-101
 
(5)删除bug分支
> git branch rm bug-101

当项目还未完成时，需要修复当前bug，而且项目尚未提交（add）,则可以将工作现场**储藏**起来。
> git stash

查看工作现场：
> git stash list

恢复工作现场：
> (1)git stash apply：

     恢复后但stash的内容不删除，需要手动删除（git stash drop）

> (2)git stash pop:

    恢复工作区的同时删除stash内容
PS：多次使用stash，恢复时先<font color=#000ff>```git stash list ```</font>,然后恢复指定的stash，使用<font color=#000ff>```git stash apply stash@{num}```</font>

**5、Feature分支**

开发新功能，则建立一个新的分支feature，但是由于需求变更，该功能不需要了，需要强制删除这个分支：
> git branch -D feature//强制删除没用合并过的分支

**6、多人协作**

查看远程仓库：
> git remote 

查看详细信息
> git remote -v

推送分支：
> git push origin master/<指定分支>

哪些分支需要推送呢？

> （1）<font color=red>`master`</font>分支是主分支，要与远程同步；
> 
> （2）<font color=red>`dev`</font>分支是开发分支，团队开发人员都在上面工作，所以需要远程同步
> 
> （3）bug分支只需要在本地修复即可
> 
> （4）feature分支是否推送到远程，取决于你是否和你的小伙伴合作在上面开发

抓取分支：
> 获取远程的dev分支：
> git checkout -b dev origin/dev

若远程端的分支与本地有冲突，则先pull下来，然后解决冲突：
> git branch --set-upstream-to=origin/dev dev  //此处需要指定本地与远程分支的链接
> git pull 
#so#
多人协作的工作模式通常是这样的：
<pre>
1、首先，可以试图用git push origin < branch-name>推送自己的修改；
2、如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
3、如果合并有冲突，则解决冲突，并在本地提交；
4、没有冲突或者解决掉冲突后，再用git push origin < branch-name>推送就能成功！
5、如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to < branch-name> origin< branch-name>。
</pre>
这就是多人协作的工作模式，一旦熟悉了，就非常简单。


**7、Rebase**

-rebase操作可以将本地未push的分叉提交历史整理成直线。

-rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

####标签管理
发布一个版本时先打一个标签<tag>，指向某个commit
标签就是为了让开发者更好的记着commit的版本

**1、创建标签**

> git tag \<name> //默认标签是打在最新提交的commit上。

查找历史版本：

> git log --pretty=oneline --abbrev-commit

对历史版本打标签
> git tag \<name> \<对应commit的版本号前六位>

查看所有标签
> git tag //标签是按照字母顺序排序

查看标签信息：
> git show <tagname>

创建带说明的标签：(-a(指定标签名) -m（指定说明文字）)
> git tag -a v1.1 -m "REMARK" \<commit id>


**2、操作标签**

删除标签
> git tag -d \<TagVersion>

推送标签到remote
> git push origin \<TagVersion>

一次性推送所有标签
> git push origin --tags

远程删除标签
> （1）从本地删除:git tag -d \<TagVersion>
> （2）从远程删除：git push origin :refs/tags/\<TagVersion>

####小结：
> 看完教程，相信你已对git有了一定的认知，学习后，会使你工作效率大增，谢谢观看。
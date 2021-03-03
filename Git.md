# Git

## Git简介

Git是Linus用**C**写的分布式版本管理系统.

集中式:版本库存放在中央服务器,必须联网(Problem)

分布式:每个人电脑上都是完整的版本库,因此比集中式**安全性高**

> 集中式:
>
> * CVS[^1]:最早的开源且免费的集中式版本控制系统<由于自身设计问题,会造成提交文件不完整,版本库莫名损坏的情况
> * SVN[^2]:同样开源且免费,修正了CVS的一些稳定性问题,是目前用得最多的集中式版本控制系统 
> * ClearCase:IBM的,收费,又大又笨

> 分布式:
>
> * Git,别的都是臭鱼烂虾

[^1]: Concurrent Versions System
[^2]:Apache Subversion

#### 创建版本库

版本库:*repository*

第一步,选一个地方,创建一个空目录

```
$ mkdir Doc
$ cd Doc
$ pwd
/c/Users/陆昱宽/Desktop/DOC
```

`pwd`命令用于显示当前目录,在我的电脑上,这个仓库位于`/c/Users/陆昱宽/Desktop/DOC`.

第二步,通过`git init`命令把这个目录变成git可以管理的仓库

```
$ git init
Initialized empty Git repository in /c/Users/陆昱宽/Desktop/DOC/.git/
```

仓库建好了,而且是空的. 当前目录下多了个`.git`的目录,这个目录是Git来跟踪管理版本库的,不要乱碰.

`.git`目录默认是隐藏的,用`ls -ah`命令就能看见

####  把文件添加到版本库

所有版本控制系统,只能跟踪文本文件的改动,比如txt,网页,代码等. 而图片,视频这些二进制文件,虽然也能由版本控制系统管理,但没法跟踪文件的变化,就是说知道改了,但不知道改了啥. 

微软的Word格式是二进制格式,所以版本控制文件没法跟踪Word文件的改动. Windows自带的记事本在保存UTF-8的文件时,会自动在其开头添加0xefbbbf（十六进制）的字符,因此会有许多问题,建议使用Notepad++ ,编码设为UTF-8 without BOM



编写一个`Git.md`文件,放到`Doc`目录下(子目录也行)

1. 先add

`$ git add Git.md`

执行上面的命令,没有任何反馈,OK了,说明添加成功

2. 再commit

```
$ git  commit -m'1
[master 45a4a38] 3
 1 file changed, 46 insertions(+)
 create mode 100644 readme.txt
```

`46 insertions`：插入了46行内容

* Q:如果输入`git add Git.md`，得到错误`fatal: pathspec 'Git.md' did not match any files`。

  A：添加某个文件时，该文件必须在当前目录下存在，用`ls`或者`dir`命令查看当前目录的文件，看看文件是否存在，或者是否写错了文件名。



## 基本操作

### 提交和查看修改

我们修改Git.md文件,运行`git.status`看看结果:

```

$ git statusOn branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    "\346\227\245\350\256\260.md"

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        Diary.md
        "\344\271\220\350\260\261.md"

no changes added to commit (use "git add" and/or "git commit -a")
```

`git.status`命令可以展示仓库当前的状态,上面的输出告诉我们,`Git.md`被修改过了,但还没有准备提交的修改.

用`git  diff Git.md`能看到具体修改了什么内容:

```
$ git diff
diff --git "a/\346\227\245\350\256\260.md" "b/\346\227\245\350\256\260.md"
deleted file mode 100644
index 4db3376..0000000
--- "a/\346\227\245\350\256\260.md"
+++ /dev/null
@@ -1,179 +0,0 @@
-　# Diary
-
-## 12 / 25
-
-　　圣诞夜中了两棵树,一棵二叉搜索树,一棵AVL树,另一棵B树没有开工,忙碌的一天。
-
-
-
-　## 12/26
-
-　　昨天凡人修仙传看到四点, 今天本打算写完微积分和计基的,但是没忍住看了一天小说
```

`git diff`顾名思义就是查看difference，显示的格式正是Unix通用的diff格式

知道了对`Git.md`作了什么修改后,再把它提交到仓库就放心多了. 提交修改和提交新文件一样是两步,

1. `git add`

   

```
$ git add Git.md
```

没有任何反应,在执行`git commit`之前,我们再运行`git status` 看看当前仓库的状态:

```
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   Git.md
```

`git status`告诉我们,将要被提交的修改包括`Git.md` ,下一步就能放心提交了:

```
$ git commit -m"4"
[master 4553e0a] 4
 1 file changed, 77 insertions(+), 1 deletion(-)
```

提交后,再用`git status`看看仓库的当前状态:

```
$ git status
On branch master
nothing to commit, working tree clean
```

Git告诉我们当前没有需要提交的修改,且工作目录是干净(working tree clean)的.

**小结**

*  要随时掌握工作区的状态,使用`git status`命令
* 如果`git status`告诉你文件有被修改过,用`git diff 文件名` 可以查看修改内容
* `commit`的message千万不能有中文,否则会乱码

### 版本回退

先提交文件,message为"origin";再输入"初次修改"并提交,message为"chucixiugai";再输入"再次修改"
并提交,message为"再次修改".

现在,`Git.md`一共有三个版本(origin之前的不算)被提交到repository里了,

版本1:origin

```

```

(啥都没写)

版本2:chucixiugai

```
初次修改
```

版本3:zaicixiugai

```
再次修改
```

我们不可能记住一个文件每次都改了什么内容,版本控制系统肯定有某个命令可以告诉我们历史记录,Git中用`git log`命令查看:

```
$ git log
commit 028637e47a974357debe623e8bb4d0ca5053db87 (HEAD -> master)
Author: 陆昱宽 <191820133@ smail.nju.edu.cn>
Date:   Sun Feb 28 23:41:08 2021 +0800

    zaicixiugai

commit cdd92a630141982791273c123d60b3ce0ed09932
Author: 陆昱宽 <191820133@ smail.nju.edu.cn>
Date:   Sun Feb 28 23:40:30 2021 +0800

    chucixiugai

commit 914f04abce43f4517121ba10957d89bd9658432e
Author: 陆昱宽 <191820133@ smail.nju.edu.cn>
Date:   Sun Feb 28 23:39:31 2021 +0800

    origin
```

`git log`命令显示最近到最远的全部提交日志,我们看最近三次,最近一次是`zaicixiugai`,上一次是`chuxixiugai`,再上一次是`origin`. 如果嫌输出信息太多不太好看,可以加上`--pretty=oneline`参数:

```
$ git log --pretty=oneline
028637e47a974357debe623e8bb4d0ca5053db87 (HEAD -> master) zaicixiugai
cdd92a630141982791273c123d60b3ce0ed09932 初次修改
914f04abce43f4517121ba10957d89bd9658432e origin
```

 我们看到许多类似`028637e`的`commit id`(版本号),这是一个SHA1计算出的非常大的数字,用十六进制表示. SVN的版本号是1,2,3,4递增,因为SVN是集中式. Git是分布式,号码容易不够,所以用这种方式

每提交一个新版本，实际上Git就会把它们自动串成一条时间线。如果使用可视化工具查看Git历史，就可以更清楚地看到提交历史的时间线

现在我们把`Git.md`回退到上个版本`chucitijiao`. 首先,Git必须知道当前版本是哪个版本,在Git中,用`HEAD`(小写也可以)表示**当前版本**,即最近的提交`02863`,上个版本就是**`HEAD^`**,上上个版本就是`HEAD^^`,以此类推. 往前100个版本数不过来,可以写成**`HEAD~100`**.

用 `git reset`命令:

```
$ git reset --hard HEAD^
HEAD is now at cdd92a6 chucitijiao
```

,`--hard`参数的意义之后再讲.  

OK,已经被还原了

现在用`git log`看看当前版本库的提交日志:

```
$ git log
commit cdd92a630141982791273c123d60b3ce0ed09932 (HEAD -> master)
Author: 陆昱宽 <191820133@ smail.nju.edu.cn>
Date:   Sun Feb 28 23:40:30 2021 +0800

    chucixiugai
    
commit 914f04abce43f4517121ba10957d89bd9658432e 
Author: 陆昱宽 <191820133@ smail.nju.edu.cn>
Date:   Sun Feb 28 23:39:31 2021 +0800

    origin
```

我们看不到最近的那个版本`zaicixiugai`了! 好比时间从21世纪穿越回了10世纪,当然看不到后面的历史了! 如果想回去,就要用`commit id`. 

1. 如果还没关掉GIt窗口,可以把窗口往上翻,找到那个`zaicixiugai`的`commit id`是`028637e...`,于是可以指定回到未来的某个版本:

```
$ git reset --hard 0286
HEAD is now at 028637e zaicixiugai
```

版本号没必要写全,写前几位. Git会自动去找. 

OK,已经回到未来了.

2. 如果已经关掉窗口了,Git中有`git reflog`记录你的每一次命令:

```
$ git reflog --pretty=oneline
028637e (HEAD -> master) HEAD@{0}: reset: moving to 0286
914f04a HEAD@{1}: reset: moving to head^
cdd92a6 HEAD@{2}: reset: moving to HEAD^
028637e (HEAD -> master) HEAD@{3}: commit: zaicixiugai
cdd92a6 HEAD@{4}: commit: 初次修改
914f04a HEAD@{5}: commit: origin
```

**小结**

* `HEAD`指向的版本就是当前版本,这是个指针. 版本穿梭使用`git reset --hard commit_id`
* 穿梭前,用`git log`可以查看提交历史,以便确定要回退到哪个版本.
* 要回到未来,可以用`git reflog`来确定要回到未来的哪个版本.
* 如果commit（提交）比较多，git log 的内容就会比较多；当满屏放不下，就会显示冒号，回车（往下滚一行）、空格（往下滚一页）可以继续查看剩余内容；**退出**：英文状态下 按 **q** 可以退出git log 状态。

### 工作区和暂存区

Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念.

*工作区(Working directory)*
就是在电脑里能看到的目录,如`Doc`文件夹就是一个工作区.

*版本库(Eepository)*
工作区有一个隐藏目录`.git`,它不算作工作区,而是Git的版本库.

Git的版本库里存了许多东西,其中最重要的就是称为*stage*(或*index*)的**暂存区**,还有Git为我们自动创建的第一个**分支**`master`,以及指向`master`的一个**指针**叫`HEAD` 

(所以版本库(包括暂存区和分支们)都在工作区里面,只是不算作工作区)

![git-repo](https://www.liaoxuefeng.com/files/attachments/919020037470528/0)

分支和`HEAD`的概念暂且不表.

前面讲了我们把文件添加剂Git版本库时,是分两步的:

第一步用`git add`把文件修改添加到**暂存区**(stage)

第二步用`git commit`把**暂存区**的**所有内容**提交到**当前分支**

因为我们创建Git版本库时,Git为我们自动创建了一个`master`分支,所以,现在`git commit`就是往`master`分支上提交更改.

需要提交的文件统统放到暂存区,然后,一次性提交暂存区(stage)的所有修改到当前分支

举例,先建个`readme.txt`提交到版本库,再在工作区(即Doc这个文件夹)里新增一个`LICENSE`文本文件,再对`readme.txt`做些修改(内容都随意). 先用`git status`看看状态:

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   readme.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        LICENSE.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Git告诉我们,`readme.txt`被修改了,这个修改没有被添加到暂存区,遑论分支了( changes not staged for commit). 而`LICENSE`这个文件还从来没被添加(add)过,所以其状态是`Untracked`. 由于没有修改被提交到暂存区,暂存区就是空的( no changes added to be commit).

现在用两次`git add`把把`readme.txt`和`LICENSE`都添加后，用`git status`再查看一下：

```
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   LICENSE.txt
        modified:   readme.txt
```

现在,暂存区状态变成这样了:

![git-stage](https://www.liaoxuefeng.com/files/attachments/919020074026336/0)



所以,`git add`命令就是把要提交的所有修改放到暂存区(stage),然后,执行`git commit`可以一次性把暂存区所有修改提交到分支. (暂存区也就被清空了),因此

![git-stage-after-commit](https://www.liaoxuefeng.com/files/attachments/919020100829536/0)



一旦**提交**(注意是`commit`) 后,如果你对工作区又没有做任何修改,那么**工作区**就是clean的:

```
$ git status
On branch master
nothing to commit, working tree clean
```

* 关于`git diff`:

  如果是输入`git diff`，查看到的是**工作区和暂存区**(上次git add 的内容)的不同，如果是`git diff --cached`，查看到的是**暂存区和HEAD**的不同。
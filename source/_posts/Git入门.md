## 1. 创建版本库


1. 创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录：
2. 通过git init命令把这个目录变成Ｇit可以管理的仓库: git init
3. 瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），
	细心的读者可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，
	没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。

## 2. 版本库添加文件
 我们了解下版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等，
Git也不例外。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了
一个单词“Windows”。而图片、视频这些二进制文件，虽然也能由版本控制系统理，但没法跟踪文件的变化，
只能把二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。

----------


1. 用命令git add告诉Git，把文件添加到仓库：git add readme.txt
2. 提交文件：git commit -m "add 3 files."

## 3. 查看当前仓库状态
**git status**：命令可以让我们时刻掌握仓库当前的状态

## 4. 查看差异
    git diff readme.txt 

## 5. 查看历史版本记录
**git log**命令显示从最近到最远的提交日志

## 6. 版本回退
每提交一个新版本，实际上Git就会把它们自动串成一条时间线。现在准备把readme.txt回退到上一个版本，也就是“add distributed”的那个版本，怎么做呢？

　　

1. 首先，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交3628164...882e1e0（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。    

2. 现在，我们要把当前版本“append GPL”回退到上一个版本“add distributed”，就可以使用git reset命令：

    $ git reset --hard HEAD^
    HEAD is now at ea34578 add distributed


## 7. 重新恢复到新版本


1. 最新的那个版本append GPL已经看不到了！好比你从21世纪坐时光穿梭机来到了19世纪，想再回去已经回不去了，肿么办？

2. 只要右侧环境还在，就可以找到那个append GPL的commit id是3628164...，于是就可以指定回到未来的某个版本：
    
    $ git reset --hard 3628164
    HEAD is now at 3628164 append GPL


## 8. 查看文本内容
$ cat readme.txt.

## 9. 命令记录
1. git reflog：用来记录你的每一次命令


## 10. 工作区
工作区：就是你在电脑里能看到的目录,learngit文件夹就是一个工作区，比如我们环境中当前的目录。

## 11. 版本库和暂存区
1. **版本库**: 工作区有一个隐藏目录.git 这个不算工作区，而是Git的版本库。

1. **暂存区**：英文叫stage,或index。一般存放在git 目录下的index文件(.git/index)中，所以我们把暂存区时也叫作索引(index).

1. Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD


## 12 版本库添加文件时的步骤
1. 第一步是用git add把文件（**工作区**的）添加进去，实际上就是把文件修改添加到**暂存区**；
2. 第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支（**仓库**）。

    因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以现在git commit就是往master分支上提交更改。Git是如何跟踪修改的，每次修改，如果不add到暂存区，那就不会加入到commit中。

## 13 管理修改
把需要进行提交的修改add到暂存区中，最后会在commit提交时git将修改放入到仓库中

## 14. 撤销修改


- 如果你在readme.txt中加入了一行文件，又感觉不好，你可以删除新加的，恢复到原来的。



- Git会告诉你，git checkout -- file可以丢弃工作区的修改：
- `git checkout -- readme.txt`
- 意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
	- 一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
	- 一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
	- 总之，就是让这个文件回到最近一次git commit或git add时的状态。

## 15. 修改总结
1. 当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。
2. 当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步：
	1. 第一步用命令`git reset HEAD file`，就回到了1；
	2. 第二步按1操作。

1. 已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过**前提是没有推送到远程库**

## 16. 删除文件
   

1.  `rm test.txt`：　命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。
2.  这个时候，Git知道你删除了文件，因此，工作区和版本库就不一致了，git status命令会立刻告诉你哪些文件被删除了：
3.  现在你有两个选择，
	1.  一是确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit
	2.  另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：`$ git checkout -- test.txt`

1. git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

## 17. 远程仓库
1. ssh方式连接远程仓库
	1. 创建SSH Key。在当前目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：`ssh-keygen -t rsa -C "youremail@example.com"`
	2. 你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
	3. 登陆GitHub，打开“Account settings”，“SSH Keys”页面：

## 18. GitHub创建新仓库
1. GitHub创建一个Git仓库,并且本地仓库与此仓库进行远程同步，此仓库既可以作为备份，又可以让其他人通过该仓库来协作。

## 19. 关联远程仓库


1. `git remote add origin git@github.com:onlyone/learngit.git`：请千万注意，把上面的onlyone替换成你自己的GitHub账户名，否则，你在本地关联的就是我的远程库，关联没有问题，但是你以后推送是推不上去的，因为你的SSH Key公钥不在我的账户列表中。

## 20. 本地内容推送远程仓库
1. 本地库的所有内容推送到远程库上：`git push -u origin master`


2. 把本地库的内容推送到远程，用git push命令，实际上是把当前分支master推送到远程。由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

1. 从现在起，只要本地作了提交，就可以通过命令：`git push origin master`：把本地master分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！

1.**总结**： 要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；关联后，使用命令git push -u origin master第一次推送master分支的所有内容；此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；

## 21. 第一次SSH警告
1. `The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.`
2. 这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。

## 22. 从远程库克隆

1. 从远程库克隆,就需要我们先创建远程库，在github创建一个新的gitskills仓库，我们勾选Initialize this repository with a README，这样GitHub会自动为我们创建一个README.md文件。创建完毕后，可以看到README.md文件：`git clone git@github.com:michaelliao/gitskills.git`

1. 你也许还注意到，GitHub给出的地址不止一个，还可以用github.com/onlyone/gitskills.git这样的地址。实际上，Git支持多种协议，默认的git: //使用ssh，但也可以使用https等其他协议。

1. 注意：要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。

## 23. 分支管理


1. 在版本回退里，你已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。

1. 一开始的时候，master分支是一条线，Git用master指向最新的提交，再用HEAD指向master，就能确定当前分支，以及当前分支的提交点

1. 每次提交，master分支都会向前移动一步，这样，随着你不断提交，master分支的线也越来越长，当我们创建新的分支，例如dev时，Git新建了一个指针叫dev，指向master相同的提交，再把HEAD指向dev，就表示当前分支在dev上：



----------
1. 现在对工作区的修改和提交就是针对dev分支了，比如新提交一次后，dev指针往前移动一步，而master指针不变：
2. 假如我们在dev上的工作完成了，就可以把dev合并到master上。Git怎么合并呢？最简单的方法，就是直接把master指向dev的当前提交，就完成了合并：
3. 所以Git合并分支也很快！就改改指针，工作区内容也不变！
4. 合并完分支后，甚至可以删除dev分支。删除dev分支就是把dev指针给删掉，删掉后，我们就剩下了一条master分支：

## 24. 创建分支
1. 首先，我们创建dev分支，然后切换到dev分支：`git checkout -b dev`
2. git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：`git branch dev` + `git checkout dev`
3. 然后，用git branch命令查看当前分支，git branch命令会列出所有分支，当前分支前面会标一个*号：`git branch`
4. 然后提交：`git add readme.txt `  +  `git commit -m "branch test"`
5. dev分支的工作完成，我们就可以切换回master分支：`git checkout master`
6. 切换回master分支后，再查看一个readme.txt文件，刚才添加的内容不见了！因为那个提交是在dev分支上，而master分支此刻的提交点并没有变：

## 25. 合并分支
1. 我们把前面dev分支的工作成果合并到master分支上：`git merge dev`
2. it merge命令用于合并指定分支到当前分支。合并后，再查看readme.txt的内容，就可以看到，和dev分支的最新提交是完全一样的。

## 26. 删除分支
1. 合并完成后，就可以放心地删除dev分支了：`git branch -d dev`
2. 删除后，查看branch，就只剩下master分支了：`git branch`
3. 因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在master分支上工作效果是一样的，但过程更安全。

## 27. 总结分支指令
- 查看分支：`git branch`
- 创建分支：`git branch <name>`
- 切换分支：`git checkout <name>`
- 创建+切换分支：`git checkout -b <name>`
- 合并某分支到当前分支：`git merge <name>`
- 删除分支：`git branch -d <name>`

## 28. 产生冲突
- 当我们进行合并分支往往会产生冲突。
1. 在准备新的feature1分支，继续我们的新分支开发：`$ git checkout -b feature1`
2. 修改readme.txt最后一行，改为Creating a new branch is quick AND simple.
3. 在feature1分支上提交：`$ git add readme.txt`
4. `$ git commit -m "AND simple"`
5. 切换到master分支：`$ git checkout master`
6. Git还会自动提示我们当前master分支比远程的master分支要超前1个提交。
7. 在master分支上把readme.txt文件的最后一行改为Creating a new branch is quick & simple.提交：`git add readme.txt `
8. `$ git commit -m "& simple"`
9. 此时，如果master和feature1合并，那么就可能产生冲突

## 29. 解决冲突
- Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有冲突，执行git merge feature1,在看readme.txt：
	- <<<<<<< HEAD
	- Creating a new branch is quick & simple.
	- =======
	- Creating a new branch is quick AND simple.
	- >>>>>>> feature1
- 我们把冲突的内容修改为Creating a new branch is quick and simple.，提交：
	- `$ git add readme.txt `
	- `$ git commit -m "conflict fixed"`

- 用带参数的git log也可以看到分支的合并情况：`$ git log --graph --pretty=oneline --abbrev-commit`
- 最后，删除feature1分支：`$ git branch -d feature1`
- 冲突解决，最后，删除feature1分支 `git branch -d feature1`，当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

## 30. bug分支
- 　　如果你有一个bug任务，你想创建一个分支issue-101来修复它，但是你当前正在dev上进行的工作还没有完成而不能提交，bug需要现在修复，所以现在你需要暂停dev上工作，Git提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作：`$ git stash`。
- 　　假定需要在master分支上修复，就从master创建临时分支：
	- 　　`$ git checkout master`
	- 　　`$ git checkout -b issue-101`

- 　现在修复bug，需要把“Git is free software ...”改为“Git is a free software ...”，然后提交：
	- 　`$ git add readme.txt` 
	- 　`$ git commit -m "fix bug 101"`
- 　修复完成后，切换到master分支，并完成合并，最后删除issue-101分支：
	- 　`$ git checkout master`
	- 　`$ git merge --no-ff -m "merged bug fix 101" issue-101`
	- 　`$ git branch -d issue-101`　

- 　Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：
	- 　一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；
	- 　另一种方式是用git stash pop，恢复的同时把stash内容也删了：
## 30. Feature分支
- 在软件开发中，总会添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。
- 现在新功能开发代号为Vulcan: `$ git checkout -b feature-vulcan`
- 开发完毕，添加并提交：
	- `$ git add vulcan.py`
	- `$ git commit -m "add feature vulcan"`

- 切回dev，准备合并：`$ git checkout dev`
- 一切顺利的话，feature分支和bug分支是类似的，合并，然后删除。


1. 由于种种原因，此功能又不需要了，现在这个分支需要就地销毁：`$ git branch -d feature-vulcan`
2. 销毁失败。Git友情提醒，feature-vulcan分支还没有被合并，如果删除，将丢失掉修改，如果要强行删除，需要使用命令`git branch -D feature-vulcan`。
3. 　现在我们强行删除：`$ git branch -D feature-vulcan`
4. 　注意：开发一个新feature，最好新建一个分支；如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。

## 31. 推送分支
- 　当你从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且远程仓库的默认名称是origin。
- 　　要查看远程库的信息，用`git remote`,或者，用`git remote -v`显示更详细的信息：
- 　　推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上： `git push origin master`
- 　　　如果要推送其他分支，比如dev，就改成: `git push origin dev`
- 　　　分支总结
	- 　　　master分支是主分支，因此要时刻与远程同步；
	- 　　　dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
	- 　　　bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
	- 　　　feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

## 32. 多人协作
- 　多人协作时，大家都会往master和dev分支上推送各自的修改。当你的同事也克隆一份此项目从远程库，默认情况下，只能看到本地的master分支。现在，你的同事要在dev分支上开发，就必须创建远程origin的dev分支到本地，于是他用这个命令创建本地dev分支：`$ git checkout -b dev origin/dev`
- 　现在，他就可以在dev上继续修改，然后，时不时地把dev分支push到远程，并且已经向origin/dev分支推送了他的提交，这时你也对同样的文件作了修改，并试图推送，推送失败，因为你的同事的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送，git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接。
- 　这回git pull成功，但是是合并有冲突，需要手动解决，解决的方法和分支管理中的解决冲突完全一样。解决后，提交，再push：`$ git commit -m "merge & fix hello.py"`
- 　`$ git push origin dev`
- 　因此，多人协作的工作模式通常是这样：
	- 　首先，可以试图用git push origin branch-name推送自己的修改；
	- 　如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
	- 　如果合并有冲突，则解决冲突，并在本地提交；
	- 　没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！
	- 　如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。

## 33. 标签
1. **标签的作用**
	1. 发布版本时，通常先在版本库中打一个标签，这样，就唯一确定了打标签时刻的版本。无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照。Git的标签虽然是版本库的快照，但其实它就是指向某个commit的指针（跟分支很像，但是分支可以移动，标签不能移动），所以，创建和删除标签都是瞬间完成的。

1. **创建标签**
	1. 首先，切换到需要打标签的分支上：`$ git checkout master`
	2. 然后，敲命令git tag <name>就可以打一个新标签：`$ git tag v1.0`
	3. 默认标签是打在最新提交的commit上的。还可以对历史提交打上标签，只要找到历史提交的commit id，然后打上就可以了，例如要对add merge这次提交打标签，它对应的commit id是6224937，输入命令：`$ git tag v0.9 6224937`
	4. 还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：`$ git tag -a v0.1 -m "version 0.1 released" 3628164`
	5. 用命令git show 可以看到说明文字：`$ git show v0.1`
	6. 签名采用PGP签名，因此，必须首先安装gpg（GnuPG），如果没有找到gpg，或者没有gpg密钥对，就会报错：`gpg: signing failed: secret key not available`
	7. 如果报错，请参考GnuPG帮助文档配置Key。
		1. 命令`git tag <name>`用于新建一个标签，默认为HEAD，也可以指定一个commit id；
		2. `git tag -a <tagname> -m "blablabla..."`可以指定标签信息；
		3. `git tag -s <tagname> -m "blablabla..."`可以用PGP签名标签；
		4. 命令git tag可以查看所有标签。
1. **操作标签**
	1. 如果标签打错了，也可以删除：`$ git tag -d v0.1`
	2. 因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。
	3. 如果要推送某个标签到远程，使用命令`git push origin <tagname>: `
	4. `$ git push origin v1.0`
	5. 或者，一次性推送全部尚未推送到远程的本地标签：`$ git push origin --tags`
	6. 如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：`$ git tag -d v0.9`
	7. 然后，从远程删除。删除命令也是push，但是格式如下：`$ git push origin : refs/tags/v0.9`
	8. 要看看是否真的从远程库删除了标签，可以登陆GitHub查看。
	9. 总结：
		1. `git push origin <tagname>`可以推送一个本地标签；
		2. `git push origin --tags`可以推送全部未推送过的本地标签；
		3. `git tag -d <tagname>`可以删除一个本地标签；
		4. `git push origin : refs/tags/<tagname>`可以删除一个远程标签。

## 34. github使用
- GitHub不仅是免费的远程仓库，个人的开源项目，可以放到GitHub上，而且GitHub还是一个开源协作社区，通过GitHub，既可以让别人参与你的开源项目，也可以参与别人的开源项目。

- 在GitHub上，利用Git极其强大的克隆和分支功能，人们可以自由参与各种开源项目。比如人气极高的bootstrap项目，这是一个非常强大的CSS框架，在它的项目主页，点“Fork”就在自己的账号下克隆了一个bootstrap仓库，然后，从自己的账号下clone。一定要从自己的账号下clone仓库，这样你才能推送修改。如果从bootstrap的作者的仓库地址git@github.com:twbs/bootstrap.git克隆，因为没有权限，你将不能推送修改。

- Bootstrap的官方仓库twbs/bootstrap、你在GitHub上克隆的仓库my/bootstrap，以及你自己克隆到本地电脑的仓库

- 如果你希望bootstrap的官方库能接受你的修改，你就可以在GitHub上发起一个pull request。

## 35. git忽略文件
- 　有些时候我们需要把一些文件例如：保存了数据库密码的配置文件放在Git目录下，但又不提交，那么需要我们在Git工作区的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。

- 不需要从头写.gitignore文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接在线浏览：https://github.com/github/gitignore

- 忽略文件的原则是：
	- 忽略操作系统自动生成的文件，比如缩略图等；
	- 忽略编译生成的中间文件、可执行文件等，也就是如果一个文件是通过另一个文件自动生成的，那自动生成的文件就没必要放进版本库，比如Java编译产生的.class文件；
	- 忽略你自己的带有敏感信息的配置文件，比如存放口令的配置文件。

## 36. git使用别名


- 配置别名其实就是把命令重新设置简单些，方便输入，例如：如果输入git st就表示git status：`$ git config --global alias.st status`

- 现在都用co表示checkout，ci表示commit，br表示branch：
	- `$ git config --global alias.co checkout`
	- `$ git config --global alias.ci commit`
	- `$ git config --global alias.br branch`
	- --global参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。

## 37. 配置文件
- 配置Git的时候，加上--global是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。

- 配置文件放哪了？每个仓库的Git配置文件都放在.git/config文件中：
- 别名就在[alias]后面，要删除别名，直接把对应的行删掉即可。
- 而当前用户的Git配置文件放在用户主目录下的一个隐藏文件.gitconfig中：配置别名也可以直接修改这个文件，如果改错了，可以删掉文件重新通过命令配置。

## 38. 搭建Git服务器
- 搭建Git服务器需要准备一台运行Linux的机器，强烈推荐用Ubuntu或Debian，这样，通过几条简单的apt命令就可以完成安装。

- 假设你已经有sudo权限的用户账号，下面，正式开始安装。

- 第一步，安装git：`$ sudo apt-get install git`

- 第二步，创建一个git用户，用来运行git服务：`$ sudo adduser git`

- 第三步，创建证书登录：收集所有需要登录的用户的公钥，就是他们自己的id_rsa.pub文件，把所有公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个。

- 第四步，初始化Git仓库：先选定一个目录作为Git仓库，假定是/srv/sample.git，在/srv目录下输入命令：`$ sudo git init --bare sample.git`
- 　Git就会创建一个裸仓库，裸仓库没有工作区，因为服务器上的Git仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的Git仓库通常都以.git结尾。然后，把owner改为git：`$ sudo chown -R git: git sample.git`

- 第五步，禁用shell登录：出于安全考虑，第二步创建的git用户不允许登录shell，这可以通过编辑/etc/passwd文件完成。找到类似下面的一行：`git: x: 1001: 1001:,,,: /home/git: /bin/bash`
- 改为：`git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell`
- 这样，git用户可以正常通过ssh使用git，但无法登录shell，因为我们为git用户指定的git-shell每次一登录就自动退出。

- 第六步，克隆远程仓库：现在，可以通过git clone命令克隆远程仓库了，在各自的电脑上运行：`$ git clone git@server:/srv/sample.git`

## 39. 管理公钥和管理权限
- **管理公钥**：如果团队很小，把每个人的公钥收集起来放到服务器的/home/git/.ssh/authorized_keys文件里就是可行的。如果团队有几百号人，就没法这么玩了，这时，可以用Gitosis来管理公钥。

- **管理权限**：有很多不但视源代码如生命，而且视员工为窃贼的公司，会在版本控制系统里设置一套完善的权限控制，每个人是否有读写权限会精确到每个分支甚至每个目录下。因为Git是为Linux源代码托管而开发的，所以Git也继承了开源社区的精神，不支持权限控制。不过，因为Git支持钩子（hook），所以，可以在服务器端编写一系列脚本来控制提交等操作，达到权限控制的目的。Gitolite就是这个工具。

- 这里我们也不介绍Gitolite了，不要把有限的生命浪费到权限斗争中。

- 主要两点：
	- 要方便管理公钥，用Gitosis；
	- 要像SVN那样变态地控制权限，用Gitolite。











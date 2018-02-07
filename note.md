# git 笔记

## git基本命令
- 建造一个文件夹：`mkdir` 
- 建造一个文件：`touch <file name>`
- 进入指定文件夹 :`cd 文件夹`
- 删除文件夹：`rm 文件夹` \ `git rm -rf 文件夹`
- 移动文夹到:`mv file ../flie/`
- 文件重命名：`mv file1 file2`
- 显示当前文件夹路径：`pwd`
- 打印信息：`echo 信息`
- 追加信息到文件中：`echo message >> file`
- 查看文件信息：`cat file`
- 列出当前文件夹里面的文件：`ls`(可见) `ls -l -a`（隐藏）
- 返回到上一层目录：`cd ..`\ `cd ~`
- 强制退出：`ctrl+c`
- 当一页信息无法完全显示时：`j`,`k`上下翻页


### vim的简单操作
1. 进入vim模式：`vim file`
2. 按`a`进入编辑模式,`esc`退出编辑模式
3. 退出vim：在非编辑模式时，打出`:`后，保存退出`wq`，不保存退出`!q`

## 配置git
- 显示当前git配置：`git config --list`
- 配置用户名儿：`git config --global user.name "message"`
- 配置用户邮箱：`git config --global user.email "message"`
- 编辑总配置(或者查看配置情况):`vim .gitconfig`
### git 配置进阶

**一、对于使用`git status`后有不用提交的文件，但是又不能删除的文件，则可以忽略。**
1. 在仓库下`vim .gitigonre`,每一行都是一个忽略对象，如果忽略一个文件，则一行中输入：`.project`，如果忽略一类文件则：列：`*.html`,`# 后面是注释`，最后的`.gitignore`需要提交推送,在github上创建仓库时可以选择初始化忽略文件.
2. 查看忽略的文件的规则：`git check-ignore -v <file name>`
3. 强制加入忽略文件：`git add -f <file name>`  

**二、在windows提交文件时出现LF和CRLF问题配置。**
1. `git config --global core.autocrl true`  
2. `git config --global core.safecrlf false` 
3. 查看：`git config -l`  
**三、别名的使用**
1. 对`git log`打印出来的信息不直观，可以使用别名更直观一下;配置信息如下：  
  1.1 `git log --pretty=format: '%h %ad | %s%d [%an]' --graph --date=short`(%h前面是esc下面的冒号)
2. 别名配置：  
  2.1 `git config --global alias.ci commit`(ci就是commit的别名)，之后去`vim .gitconfig`里面根据格式添加更多的格式，例如上面的一长串。 
   
**四、暂缓凭证**
1. 对于https的协议，每次推送都要输入github的用户名和密码，使用暂缓凭证可以不用每次都输入密码。  
  1.1 `git config --global credential.helper wincred`之后输入两次密码就可以不用每次输入密码了。
  
## 协议
**一、本地协议**  
- 本地仓库之间的克隆：`git clone /c/wd/test.git` 远程链接的话：`git clone add origin /c/wd/test.git` 
 
**二、http协议**  
- 添加远程仓库的链接：`git remote add origin https://github.com/Xiaolincolin/test.git`     
- 克隆远程仓库的链接：`git clone https://github.com/Xiaolincolin/test.git`

**三、SSH协议**  
1. 首先得获取密钥对，在命令行敲：`ssh-keygen -t rsa -C "email"`然后一直默认，敲回车，直到密钥生产，然后去生成的目录中敲：`ls -l -a`找到`.ssh`文件夹进去再查看隐藏的文件，找到带`pub`的共玥，`cat id_rsa.pub`,复制到github网址上创建新的ssh服务。
2. 密钥生成以后就能使用ssh协议克隆和推送以及更新  
  2.1 克隆：`git clone git@github.com:user.name/repository`  
  2.2 添加ssh链接：`git remote add origin git@github.com:user.name/repository`

## 仓库
- 初始化成仓库:`git init` 
- 提交到缓存区：`git add .`(全部提交), `git add test`（只提交test），`git add -p <file name>` 选择`s`进行分割，然后分割出来要提交的选择`y`,不提交的选择`n` 
- 信息描述:`git commit -m "message"`（一行描述），`git commit -am\-a -m "message"`(当文件已经存在做修改时无需提交描述),`git commit`（格式化描述）  
- 查看状态：`git status`\ `git status -sb`(让提示信息简短)
- 查看提交信息:`git log`\ `git log --oneline`(简短),`git log --pretty=format: '%h %ad | %s%d [%an]' --graph --date=short`
- 查看某个人提交信息的内容时：`git show 哈希值（HEAD）`,`git show HEAD~数字`数字几就是第几条
- 查看某一类描述时用：`git log --grep docs(类型)`（git hi --grep docs）
- 查看本地的仓库与github仓库的Url链接情况：`git remote -v`
- 若没链接，创建链接（https协议）：`git remote add origin https://github,com/Xiaolincolin/“仓库名“`
- 推送:`git push origin master`
- 导入本地（更新）:`git pull origin master`
- 克隆：`git clone url`
- 查看git的全部子命令：`git help -a`
- 查看指定某一个文件的修改历史：`git blame <file name>`,`git blame -L 10,20 <file name>`查看某个文件的修改历史，第二个是可以查看10到20行的修改历史。这个与`git log`的区别是log查看仓库下的历史。  
- 清除未被跟踪的文件（就是没有git add的文件）:
  1. 首先`git clean -n` 列出未被跟踪的文件   
  2. 然后清除：`git clean -f`
  3. 清除被忽略的文件：`git clean -x -f`

### 查看信息的命令（提交状态）
工作区与提交版本，工作区与暂存区，暂存区与提交区的查看命令图片：
![][open]  
由上面图片：  

1. 工作目录和暂存区的区别：`git diff`
2. 暂存区与提交的最后一个版本的差异：`git diff --cached`  
3. 工作目录与提交最后一个版本差异：`git diff HEAD`
4. 提交版本中两个之间的差异：`git diff <哈希值1> <哈希值2>`或者`git diff HEAD~4 HEAD~1`
5. 查看工作区与提交区的某个版本的差异，可以在你想查看的版本中打个标签：`git tag <标签名> 哈希值（HEAD~数字）`，然后`git diff <标签名>`
6. 暂存区与标签的差异：`git diff --cached <标签>`

### 回撤操作
回撤操作有从历史退到暂存区，有暂存区退到工作区，有历史退到工作区，有从远程仓库退到工作区(不建议使用)：
![][resert]  

- 从暂存区回退到工作区：`git reset HEAD`
- 从历史版本撤回到暂存区：`git reset HEAD~数字 --soft`，数字是几代表撤回几个历史信息到暂存区。
- 直接将历史区中的提交删除：`git reset (哈希值)HEAD~数字 --hard`,则直接将到数字的版本全部删除，若后悔删除则继续执行`git reset HEAD~数字 --hard`既回退。
- 将远程仓库中的东西拽回来：`git push -f`，例如在本地仓库中修改了或者删除了一些历史版本，讲远程仓库与本地仓库保持同步，也将删除或修改一些东西。
- 将本次提价与上一次提交作为一个提交：`git commit --amend -m "message"`

#### 变基操作（将历史版本信息修改整合等）
- 将多条提交信息变成一条信息：`git rebase -i HEAD~数字`，里面如果是`s`则多条信息整合，如果用`r`则修改提交信息等等。
### 标签
- 在当前提交版本上打标签：`git tag <name>`,或者需要给标签备注信息时：`git tag <name> <哈希值或者版本值HEA~?> -m "message"`不加版本值默认最后一个版本。打上的标签可以当做哈希值用。查看标签用`git tag`,删除标签：`git tag -d <name>`
- 标签要单独推送：`git push url <tag name>`这是单个标签推送，如果要所有标签一起推送则：`git push url --tags` 
  - 当本地的标签删除后要同步到远程仓库，则：`git push url :refs/tags/<tag name>`

## 分支
### 创建分支
![][branch]





<!---  链接  -->    
[open]:gitnote/1.png
[resert]:gitnote/3.png
[branch]:gitnote/branch1.png

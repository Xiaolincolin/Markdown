# git 命令笔记第一讲

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
  

## 仓库
- 初始化成仓库:`git init` 
- 提交到缓存区：`git add .`(全部提交),`git add test`（只提交test）  
- 信息描述:`git commit -m "message"`（一行描述），`git commit -am\-a -m "message"`(当文件已经存在做修改时无需提交描述),`git commit`（格式化描述）  
- 查看状态：`git status`\ `git status -sb`(简短)
- 查看提交信息:`git log`\ `git log --oneline`(简短)
- 查看某个人提交信息的内容时：`git show 哈希值（HEAD）`
- 查看本地的仓库与github仓库的Url链接情况：`git remote -v`
- 若没链接，创建链接（https协议）：`git remote add origin https://github,com/Xiaolincolin/“仓库名“`
- 推送:`git push origin master`
- 导入本地（更新）:`git pull origin master`
- 克隆：`git clone url`

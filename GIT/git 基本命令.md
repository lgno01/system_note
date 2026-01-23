# 配置 Git 环境，用户名、邮箱、SSH密钥
## 设置Git的user name和email
  git config --global  user.name  "Gang.LI"
  git config --global user.email " gang.li @ imotion.ai "

## 如果想在当前项目中使用不同的用户名和邮箱，而不影响全局配置，可在项目目录下执行以下命令：
  git config user.name "Your Name"
  git config user.email "your.email@example.com"

-- 生成SSH密钥
  ssh-keygen -t rsa -C “ gang.li @ imotion.ai ”
  会提示输入密码， 按回车输入密码为空即可。
  会生成 id_rsa.pub
-- 添加SSH密钥到Bitbucket
  打开 id_rsa.pub 拷贝其中内容，放到 Bitbucket 账号中的SSH keys 中即可。


# 基本操作
## 初始化(创建新仓库)
git init    # 

## 删除本地仓库
rm -rf .git

## 克隆仓库到本地
-- git clone xxx   # 复制一个远程仓库并下载到本地

## 查看当前仓库状态
-- git status      # 显示当前工作目录中哪些文件发生了更改，是否已暂存，是否未被跟踪

## 将文件添加到暂存区
-- git add xxx     # 将文件xxx 放入暂存区
-- git add .       # 将当前目录下所有更改都放入暂存区

## 提交暂存区的更改，并附带提交信息
-- git commit -m "xxx"   # 提交暂存区的更改到本地仓库，并附带提交信息 xxx

## 推送代码到远程仓库
-- git push      # 将本地仓库的提交推送到远程仓库，默认推送到同名分支

## 查看工作区和暂存区的差异
-- git diff

## 查看提交历史记录
-- git log

## 查看分支列表
-- git branch     # 查看本地分支列表
-- git branch -a  # 查看所有分支列表（包含远程）

# 暂存操作
-- git stash                 # 将未提交的修改保存到Git的stash 中
-- git stash save "xxx"      # 将未提交的修改保存到Git的stash 中，并设置一个描述信息，帮助我们理解stash 中的内容。
-- git stash list            # 列出所有保存在stash 中的修改，每个stash 都有唯一的标识符。
-- git stash apply  xxx      # 将指定的stash应用到当前分支，但不会删除该stash
-- git stash pop             # 将最近保存的stash应用到当前分支，并删除该stash
-- git stash drop xxx        # 删除指定的 stash
-- git stash clear           # 删除所有的 stash
-- git stash branch xxx      # 基于stash创建一个新的分支，并将该stash应用到新的分支中

# 撤销操作
## 撤销暂存区的所有修改
-- git reset
-- git reset HEAD xxx   # 对已经在暂存区的文件，现不想提交，想再次进行修改，可用此操作把相应的文件从暂存区拉回到本地。xxx 为要操作的文件名

## 撤销暂存区指定文件的修改
-- git reset xxx           # 撤销工作区指定文件的修改

## 撤销工作区指定文件的修改
-- git checkout xxx        # 撤销工作区指定文件的修改

## 撤销指定commit号的提交修改
-- git revert xxx          # 撤销指定提交的修改

## 重置工作区、暂存区和git仓库的状态
-- git reset --hard 

## 撤销本地仓库区到暂存区
-- git reset --soft    # git commit后，将commit还原到commit之前，add之后

## 撤销暂存区到工作区
-- git reset --mixed   # git commit后，将commit还原到add之前

## 撤销本地仓库到未修改前
-- git reset --hard    # git commit后，将所有还原至未修改之前



# Submodule 相关命令
## 更新关联的 submodule
-- git submodule update --init --recursive

## 把所有的 submodule 统一切换到 XXX 分支
-- git submodule foreach git checkout xxx

## 把所有的 submodule 统一更新到最新
-- git submodule foreach git pull

## 查看各 submodule 当前 commit 号
-- git submodule

# reset hard to origin/develop
-- git reset --hard origin/develop


# 在github创建新仓库,不要勾选 Add README.md 等选项，只需要创建一个空仓库即可。并复制仓库URL

# 初始化本地git仓库
git init

# 添加所有文件到暂存区(查看状态)
git add .
git status

# 提交暂存区文件到本地仓库
git commit -m "Initial commit"

# 添加远程仓库,
git remote add origin <remote_repository_url>

# 推送本地仓库到远程仓库(-u 表示绑定本地main分支和远程origin/main分支)
git push -u origin main

# 后续推送本地仓库到远程仓库(无需-u参数)
git push
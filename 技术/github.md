# Git 常用命令指南

## 1. 克隆远程仓库到本地
使用此命令将 GitHub 上的代码下载到 VS Code 中：
`git clone https://github.com/haoxiangjia-sys/java-.git`

---

## 2. 初始化并推送到远程仓库
如果你是新建的项目，请按以下步骤操作：

* **初始化本地仓库**: 
  `git init`
* **将所有文件添加到暂存区**: 
  `git add .`
* **提交到本地仓库**: 
  `git commit -m "提交说明"`
* **关联远程 GitHub 仓库**: 
  `git remote add origin https://github.com/你的仓库地址`
* **切换主分支并推送**: 
  `git branch -M main`
  `git push -u origin main`

---

## 3. 常用终端命令
* `cd ..` —— 返回上一级目录
* `cd ~`  —— 回到用户主目录
* `cd /`  —— 回到根目录
* `pwd`   —— 显示当前工作目录 (print working directory)
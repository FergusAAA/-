# 目录
- [1. Git 基础命令](#Git 基础命令)
	- [1.1. 配置信息](#1.-配置信息)
	- [1.2. 建立工作区](#2.-建立工作区)
	- [1.3. Git 提交](#3.-Git 提交)

# Git 基础命令
## 1. 配置信息
- 配置全局用户信息
	```shell
	git config --global user.name "XXX"
	git config --global user.email 12345678@git.com
	```
- 查看配置信息
	```shell
	#查看指定的属性
	git config --global user.name
	#查看全部属性
	git config --global -l
	```
-  当前工作区的配置信息
	```shell
	#设置当前工作区的用户名
	git config user.name "XXX"
	#查看当前工作区的邮箱
	git config emil
	#查看当前工作区的全部配置信息
	git config -l
	```

## 2. 建立工作区
```shell
#在当前所在的目录下创建工作区
git init
#在当前所在的目录下创建目标文件夹，并在目标文件夹中创建工作区
git init targetFile
```

## 3. Git 提交
- status 命令: 查看当前工作区修改状态
	 ```shell
	git status
	# 以紧凑的格式输出
	git status --short
	git status -s
	```
	
- add 命令: 对指定文件开始跟踪 或 将改动加入下次commit中(加入暂存区)
	```shell
	git add .
	```
	
- .gitignore: 总会有些文件无需纳入 Git 的管理，也不希望它们总出现在未跟踪文件列表，可以使用``.gitignore``文件来管理。可以在  https://github.com/github/gitignore 中找到各个语言的``.gitignore``

- diff 命令: 查看文件修改细节

   ```shell
   #查看未暂存的文件修改
   git diff
   #查看已加入暂存区的文件修改
   git diff --staged
   ```

- commit 命令: 生成一次commit

   ```shell
   git commit -m "commit信息"
   #启动文本编辑器，输入提交说明
   git commit
   #设置默认编辑软件
   git config --global core.editor vim
   ```














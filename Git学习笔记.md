# 目录
- [1. Git 基础命令](#git-基础命令)
	- [1.1. 配置信息](#1-配置信息)
	- [1.2. 建立工作区](#2-建立工作区)
	- [1.3. Git 提交](#3-git-提交)
	- [1.4. Git 撤销操作](#4-git-撤销操作)
- [2. Git 远程仓库](#git-远程仓库)

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
   #把所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add 步骤
   git commit -a
   ```

- rm 命令: 将改动从暂存区移除

  ```shell
  #当文件已被删除，不希望继续被跟踪
  git rm
  #当强制将文件从暂存区移除，并删除该文件
  git rm -f
  #将文件从暂存区移除，放到未暂存区域
  git rm --cached
  ```

- mv 命令: 移动或重命名文件

  ```shell
  git mv xxx.xxx xxx
  ```

- log 命令: 查看提交历史

  ```shell
  #默认不用任何参数的话，git log 会按提交时间列出所有的更新，最近的更新排在最上面
  git log
  #显示每次提交的内容差异
  git log -p
  #显示最近*(数字1/2/3/4/5/6……)次提交
  git log -2
  #显示简略的统计信息
  git log --stat
  #仅在提交信息后显示已修改的文件清单
  --name-only
  #显示新增、修改、删除的文件清单
  --name-status
  #使用较短的相对时间显示（比如，“2 weeks ago”)
  --relative-date
  #按照时间限制
  --since 和 --until
  #按照作者搜索
  --author
  #按照commit提交关键字
  --grep
  #按照修改中的字符串或函数引用
  -S function_name
  #按照路径搜索(使用--分隔其他选项，放最后)
  git log --author xxx -- (路径)
  ```

## 4. Git 撤销操作

- git commit --amend: 提交完了才发现漏掉了几个文件没有添加，或者提交信息写错了
  例如，我提交完成后，发现少提交一个``A文件``,则可以

  ```shell
  #将 A文件 加入暂存区
  git add A
  #输入提交信息重新提交
  git commit --amend
  ```

- 取消暂存: git restore --staged <file>

  ```shell
  #创建两个文件
  touch 1.log
  touch 2.log
  #全部加入暂存区
  git add *
  #将2.log取消暂存
  git restore --staged 2.log
  ```

- 取消未暂存区的修改：git restore <file>

  ```shell
  #修改某个文件
  vi 1.log
  #取消文件修改
  git restore 1.log
  ```




# Git 远程仓库








# 创建仓库
[https://github.com/JoyceWang1][1]创建repository
# 提交仓库
## 首次提交
1. 本地
	```bash
	echo "# learning" >> README.md
	# 初始化目录为 git 项目
	git init
	# 加入缓存区
	git add README.md
	# 本地库提交
	git commit -m "init my learning"
	```
2. 远程
	```bash
	# 添加远程
	git remote add origin https://github.com/JoyceWang1/learning.git
	# 提交到远程
	git push -u origin master
	# 查看远程仓库
	git remote -v
	```
## 更新提交
1. 本地
	```bash
	# 加入缓存区
	git add README.md
	# 本地提交
	git commit -m "by Joyce"
	```
2. 远程
	```bash
	# 提交远程
	git push -u origin master
	```
##  忽略提交
`.gitignore`只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。
解决方法就是先把本地缓存删除（改变成未track状态），然后再提交:
```bash
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
```

[1]:	https://github.com/JoyceWang1
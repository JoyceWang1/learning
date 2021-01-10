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
	# 添加 fork
	git remote add upstream https://github.com/xiaolai/learning.git
	# 合并 upstream master
	git merge upstream/master
	
	# 提交到远程
	git push -u origin master
	git push -u origin master:master  # 覆盖远程
	# 检查远程更新
	git fetch upstream
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
	# 检查远程更新
	git fetch upstream
	# 提交远程
	git push -u origin master
	```
3. fork 更新

   ```bash
   # 添加 upstream 源 URL
   git remote add upstream URL
   # fetch  和 merge master 分支
   git fetch upstream
   git merge upstream/master
   
   # 提交到远程
   git push -u origin master
   ```

4. 

##  忽略提交

`.gitignore`只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。
解决方法就是先把本地缓存删除（改变成未track状态），然后再提交:
```bash
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
```

[1]:	https://github.com/JoyceWang1

## 慢的问题

解决国内慢的问题

````````bash
# 访问：http://github.global.ssl.fastly.net.ipaddress.com/#ipinfo 获取CDNip和域名
eg：199.232.69.194 https://github.global.ssl.fastly.net

# 访问：https://github.com.ipaddress.com/#ipinfo 获取CDNip和域名
eg：140.82.114.4 http://github.com

sudo vi /etc/hosts
199.232.69.194 https://github.global.ssl.fastly.net
140.82.114.4 http://github.com
````````


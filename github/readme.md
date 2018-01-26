## github操作详解
### 通用操作
	1.申请注册github账号
	2.登陆找到settings
	3.点击new ssh key按钮出现输入框绑定公钥（可以绑定多个，方便本地git提交到github仓库）
	4.密钥（公钥和私钥）生成
		4.1cmd命令输入ssh-keygen -t rsa -C "xxxx@qq.com"按三次回车即可生成密钥
		4.2生成密钥会提示你密钥所在文件夹
##### mac
	5.密钥文件夹查找可以在终端输入open ~/.ssh打开，也可以command+shift+g输入目录地址打开
##### pc(windows)
	5.密钥文件夹查找可以直接在Administrator/.ssh(C:\Users\Administrator\.ssh)找到
	
	6.拷贝.ssh/id_rsa.pub里的内容到new ssh key的输入框里绑定即可
	7.在终端或是git bash中输入ssh -T git@github.com 验证是否成功，如果是第一次的会提示是否continue，输入yes就会看到：You've successfully authenticated, but GitHub does not provide shell access 。这就表示已成功连上github。
	8.new repository新建项目，填写项目名字和描述然后默认就行了
	9.需要设置username和email，因为github每次commit都会记录他们。
		9.1$ git config --global user.name "your name"
		9.2$ git config --global user.email "your_email@youremail.com"
	10.给某个项目文件夹添加远程仓库地址（github）
		10.1先给这个项目文件夹git init一下（已经git初始化过的就不用了）
		10.2$ git remote add origin git@github.com:yourName/yourRepo.git
		10.3git remote -v查看是否关联成功
		10.4关联成功：
			10.4.-1最好添加.gitignore文件（内容.project（编辑器生成的操作文件）和.gitignore（忽略文件自身，这样就在git status就不会提示自身修改的））
			10.4.0git fetch
			10.4.1git add .
			10.4.2git commit -m 'xxxx'
			10.4.3git pull origin master --allow-unrelated-histories（合并远程仓库代码）
			10.4.4查看冲突文件git status(或是git status -uno)
			10.4.5删除冲突文件的冲突代码或是git -rm --cached '文件路径'移除已经add的文件(不删除物理文件，仅将该文件从缓存中删除)或是git rm --f "文件路径"（不仅将该文件从缓存中删除，还会将物理文件删除（不会回收到垃圾桶））。
			10.4.6git add .
			10.4.7git commit -m 'xxxx'
			10.4.7git push origin master（不行就git push --set-upstream origin master）
			
####git rm的说明文档
$ git rm -h
用法：git rm [<选项>] [--] <文件>...

    -n, --dry-run         演习
    -q, --quiet           不列出删除的文件
    --cached              只从索引区删除
    -f, --force           忽略文件更新状态检查
    -r                    允许递归删除（用于删除文件夹）
    --ignore-unmatch      即使没有匹配，也以零状态退出
git rm -r '文件夹路径' '文件夹路径'	可以删除多个文件夹
git rm '文件路径' '文件路径'	可以删除多个文件

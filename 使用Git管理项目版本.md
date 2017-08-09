使用Git管理项目版本
=================
##  1、git 配置
```Bash
    vagrant@homestead:~/Code$ git config --global user.name "jinhesui"
```

```Bash
    vagrant@homestead:~/Code$ git config --global user.email "980172200@qq.com"
```

```Bash
    vagrant@homestead:~/Code$ git config --global push.default simple
```

    --global 选项代表对 Git 进行全局设置
##  2、github托管项目
    生成SSH密钥

vagrant@homestead:~/Code$ ssh-keygen -t rsa -C "980172200@qq.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/home/vagrant/.ssh/id_rsa):
/home/vagrant/.ssh/id_rsa already exists.
Overwrite (y/n)? y
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/vagrant/.ssh/id_rsa.
Your public key has been saved in /home/vagrant/.ssh/id_rsa.pub.
接下来将 SSH Key 添加到 ssh-agent 中：
$ eval `ssh-agent -s`
$ ssh-add ~/.ssh/id_rsa
最后我们需要将公钥添加到 GitHub 账号，可参照下面的 GitHub 官方指南完成配置：
1.获取生成的SSH key,即这个文件 ~/.ssh/id_rsa.pub中的内容,使用cat命令将文件内容打印出来，然后再复制。
vagrant@homestead:~/Code$ cat ~/.ssh/id_rsa.pub
2.登录Github,进入个人Setting页，将复制的内容粘贴到下边的Key框中即可，然后点击Add SSH Key 按钮，这时候，会让你重新输入登录密码进行确认。
测试：
vagrant@homestead:~/Code$ ssh git@github.com
Enter passphrase for key '/home/vagrant/.ssh/id_rsa':
PTY allocation request failed on channel 0
Hi jinhesui! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
3、将本地代码推送到Github
1.Github上创建一个git仓库
我这里建的仓库地址为：
https://github.com/jinhesui/butterfly.git
2.初始化git
先切换到Code/butterfly目录下，然后进行初始化git init
vagrant@homestead:~/Code$ cd butterfly
vagrant@homestead:~/Code/butterfly$ git init
Initialized empty Git repository in /home/vagrant/Code/butterfly/.git/
3.将项目所有文件纳入到 Git 中：
vagrant@homestead:~/Code/butterfly$ git add -A
4.检查 Git 状态：
vagrant@homestead:~/Code/butterfly$ git status
上面命令将会向你输出存放在 Git 暂存区的文件，这意味着这些文件还未真正提交到 Git 中。
5.保留改动并提交：
vagrant@homestead:~/Code/butterfly$ git commit -m "Initial commit"
6.将代码上传到github
$ git remote add origin git@github.com:jinhesui/butterfly.git
$ git push -u origin master
git本地仓库首次push到远程仓库出现错误 ! [rejected] master -> master (fetch first)
解决很简单，使用强制推送命令
git push -f origin master
至此，项目已成功托管到 GitHub 上了，^_^
以后本地代码有改动，我们只需要下面三个命令即可推送到Github:
// 1、保存到暂存区：
vagrant@homestead:~/Code/butterfly$  git add -A

// 2.输入描述信息并提交到本地的 Git
vagrant@homestead:~/Code/butterfly$  git commit -m "Describ something"

// 3.将代码推送到 GitHub的主干分支
vagrant@homestead:~/Code/butterfly$ git push origin master

echo "# docs" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/jinhesui/docs.git
git push -u origin master

# git使用记录（1）——上传本地文件夹到github



#### 一般步骤：

1. 在网页端新建远程仓库，命名demo_repo，记录下此repo的ssh或者git地址
2. cd到本地项目文件夹
3. git init，在项目文件夹内生成一个.git文件夹，讲项目文件夹变成一个git可管理的文件夹
4. git add .  上传本地文件，不要漏掉 . ，.的意思是当前文件夹路径
5. （可选）git status ，查看add的文件
6. git commit -m "first commit"，first commit可替换成任何想要备注commit的字段
7. git remote add origin https://github/username/demo_repo.git，这一步是将本地项目文件夹连接到远程仓库，后面的地址为第一步新建的远程仓库的地址
8. git push -u origin master，上传文件



### 可能遇到的问题:

#### 1. OpenSSL SSL_read: Connection was reset, errno 15504:

![image-20210813103101311](C:\Users\Dell\AppData\Roaming\Typora\typora-user-images\image-20210813103101311.png)

这是服务器的SSL证书没有经过第三方机构的签署，所以报错。

**解决办法：**

```
git config --global http.sslVerify "false"
```

然后再重新执行要执行的git操作即可。



#### 2. 在push项目的时候报错， remote: Invalid username or password. fatal: Authentication failed for xxx

**解决办法：**

2.1 在自己github上找到settings

2.2 进入Developer settings

2.3 点击左侧列表中的Person access tokens

2.4 点击右侧Generate new token

2.5 生成了新的token

2.6 重新执行git push origin master

2.7 在弹窗里输入新的token

2.8 弹窗或者终端按照提示输入用户名和密码

详见：https://blog.csdn.net/u013977285/article/details/79726354



#### 3. git push origin master提交代码时报错

fatal：Authentication failed for‘https：//git……

**解决办法：**

3.1 git config --global --list查看user_name和user_email

3.2 git config --global user.name “xxx”

3.3 git config --global user.email “xxx”

3.4 再重新push



#### 4. 报错 git@github.com: Permission denied (publickey).

**解决办法：**

4.1 git config --global --list 验证邮箱与GitHub注册时输入的是否一致

4.2 设置全局用户名和邮箱：

  	git config --global [user.name](http://user.name/) “yourname”

​      git config --global user.email “email@email.com ”

4.3  ssh-keygen -t rsa -C “这里换上你的邮箱”， 然后一路回车，在出现选择时输入Y，再一路回车直到生成密钥。密钥地址在 ~/.ssh/id_rsa.pub中

4.4 到网页端git仓库添加密钥

​		settings -> SSH and GPG keys -> New ssh key ，然后将/Users/***/.ssh/id_rsa.pub粘贴到key里，-> add SSH key

4.5 测试，执行ssh -T [git@github.com](mailto:git@github.com)，测试一下通不通，通了就可以正常执行之前要执行的操作。

​       如果不通， 执行

​							ssh-agent -s

​							ssh-add ~/.ssh/id_rsa

​       然后再测试 ssh -T [git@github.com](mailto:git@github.com)通不通，一般这样就通了。


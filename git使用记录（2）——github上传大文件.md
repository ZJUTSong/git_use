# git使用记录（2）——github上传大文件



#### 网页端一般上传单个文件不能超过25M，因此需要另外有上传大文件的方法



#### 一般步骤，以上传本地文件夹到github为例：

1. git init
2. git lfs install
3. git lfs track "大文件或者文件夹的路径"
4. git add .gitatterbutes
5. git add "大文件或者文件夹的路径"
6. git commit -m "commit说明"
7. git remote add origin https://github/username/demo_repo.git，即将本地和远程仓库配对
8. ssh-keygen -t rsa -C user_email,  user_mail是注册github的email，生成密钥在~/.ssh/id_rsa.pub中
9. 打开~/.ssh/id_rsa.pub复制内容，在网页端新建SSH key并复制进去
10. 上传文件git push -u origin master



#### 注：

1. 如果本地和远程已经配对过，则7、8、9可以跳过。

2. 针对大文件上传的步骤为2、3、4，其余都和普通上传文件一样
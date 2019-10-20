# ACGN2019
这里是软院动漫社|。•ω•)っ

---

## 初次使用教程

1. 在本地创建可以放置在此账号下的ssh文件（若本身有ssh与其他github账号绑定，则需要重新利用以下语句进行新建ssh操作）:

```
ssh-keygen -t rsa -f <某个路径> -C "<自己的邮箱>"

# 建议<某个路径>部分直接使用默认路径，只修改文件名
# 例如默认路径为"~/.ssh/id_rsa"，则后续再创建ssh文件时将路径设为"~/.ssh/id_rsa_<某个后缀>"。之后可以看到我对这部分的处理
```

**注意：若已被其他github账号占用的ssh文件以默认路径存储，则不可以再在默认路径下创建id_rsa文件。否则原ssh将会被覆盖（即其他github上绑定的ssh作废）**

2. 在默认的ssh路径目录下创建config文件，将不同的ssh文件分离开。config文件内容结构如下：

```
# Madderate
Host github.com             # 自定义的host名称，用于区分不同的ssh
HostName github.com         # 目前我们只用到github，所以这项固定github.com
User Madderate              # 这项根据github的账号来设定。如添加至动漫社账号的ssh，此项应设定为NCU-ACGN
IdentityFile ~/.ssh/id_rsa  # 绑定到上述github账号的ssh文件路径（'~'代表当前用户目录，不要填写.pub文件路径）

# NCU-ACGN （结构同上，这里处理和上一块不同的ssh文件）
Host NCU-ACGN.github.com            # 自定义的host名称，用于区分不同的ssh
HostName github.com                 # 转到github
User NCU-ACGN                       # github上账号的名称
IdentityFile ~/.ssh/id_rsa_ncu_acgn # 用在这个github账号下的ssh文件路径。
                                    # 我直接通过修改ssh文件的文件名来与原来的文件进行区分

```

3. 之后创建本地git仓库（或从github上clone远程仓库至本地）：

```
# 初始化本地git仓库
# 首先需要切换到要被初始化的目录中

git init
```

```
# 将远程仓库内容clone过来
# 代码联动上面的config文件内容

git clone git@NCU-ACGN.github.com:NCU-ACGN/ACGN2019.git

# 因为为了使用添加在NCU-ACGN账号下的ssh，我直接使用NCU-ACGN.github.com来访问NCU-ACGN的仓库
# 这保证该工作区能够正常访问远程仓库（github上的仓库）
```

4. 如果不放心，可以在本地工作区目录下，利用以下命令来查看工作区的config文件是否采用了NCU-ACGN.github.com作为自己的host：

```
git config --list
```

*这条指令输入后，需要查看它的回显结果中是否有如下结果：*

```
remote.origin.url=git@NCU-ACGN.github.com:NCU-ACGN/ACGN2019.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
```

*如果出现，则说明config文件配置成功，可以正常的push上远程git仓库（github）*

5. 配置自己的用户名和邮箱。利用以下命令配置：

```
# 配置用户名
git config user.name "NCU-ACGN"     # 不知道能否使用其他名称。按理可以

# 配置邮箱
git config user.email "<你的邮箱>"   # 邮箱可以自定义，亲测
```

6. 之后将想要添加/修改的部分处理完成后，利用git add等指令添加、提交。这部分因为网上有不少现成教程，故不赘述。**推荐百度/bing/google搜索"git 廖雪峰"**

7. 然后git push，成了！


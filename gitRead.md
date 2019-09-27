# study

#### git、github、gitLab
```
- git : 是版本控制系统
- github : 用于管理版本的服务端软件 （私有的需要付费）
- GitLab : 用于管理版本的服务端软件 （免费）
```

#### git设置
```
    1. 设置用户名，邮箱  
        git config --global user.name "your name"
        git config --global user.email "your email"
    2. 查看全局设置
        git config --global --list
    
```

#### git介绍
```
    为什么用git
    1. 本地可以建立版本库
    2. 本地版控制
    3. 多主机异地协同工作
    4. 重写提交说明
    5. 更完善的分支系统
    6. 速度快

    文件三种状态：
    已修改 modified
    已暂存 staged
    已提交 commited

    查看git安装在哪
    which git 
```

#### 常用命令
```
    红色： 代表在工作区，修改了
    绿色： 代表提交到了暂存区

    初始化git仓库
    git init  或  git clone  

    // 版本管理
    git add    暂存区
    git commit -m ""    将暂存区的内容提交到版本库中（此时才是版本库）
    git rm    删除版本库中的文件

    // 查看信息
    git help
    git log   退出是  q
    git diff

    // 远程协作
    git pull   拉取到本地
    git push   推送到远程

    // 添加到缓存区之后，怎么撤回到工作区 
        1.1. git reset HEAD 1.css  将待删除的文件从暂存区恢复到工作区（改的东西还在）
        1.2. git checkout -- 1.css 将工作区的修改丢掉（！！！修改的东西被丢弃）

        2. git rm --cached 1.css 回到改之前的样子（改的东西还在）
        或者
        3. git reset HEAD 1.css  将待删除的文件从暂存区恢复到工作区（改的东西还在）
    
    // 误删除文件，怎么恢复（在工作区中）
        1. 先 git reset HEAD 1.css
        2. 再 git checkout -- 1.css 就回来了

    // 
        git config --list
        git config --local user.name "hh"
        git config user.name
    
    // 查看git的配置文件
        cat ~/.gitconfig

```

```
    git rm 的作用: 1.删除文件 ，2. 被删除的文件被添加到缓存区
    rm 系统命令删除： 只删除文件，没有加到暂存区， 需要通过 git add 1.css 加入才能 恢复

    git mv 1.txt 2.txt  同文件夹下是重命名，不同就是移动

    git commit --amend -m "修改上次提交时的提交信息"

    git log -2 显示2条日志
    git log --pretty=oneline
    git log --pretty=format:"%h-%an,%a:%s"
```

#### .gitignore
```
    单独创建这个文件，在里面添加不需要被追踪的文件，这样就会忽略这些文件，这样就不会添加到版本库中
    *.b   忽略 所有以 .b 结尾的
    !a.b  a.b除外
    /3.txt  只忽略根目录下的TODO文件，不包含子目录下的/3.txt
    /**/3.txt
    build/  忽略这个文件下的所有文件
```

####  分支
```
    git branch  查看分支
    git branch new_branch  创建新的分支 （分支的内容相同）
    git checkout new_branch  切换分支
    git branch -d new_branch 删除分支

    git checkout -b new_branch 创建并切换到新分支

    git merge new2  合并分支

    HEAD ：指向的是当前的分支
    master: 指向的是提交

    git log --graph  图形查看日志
```

#### 版本回退
```
    git log --graph --pretty=oneline --addrev-commit

    回退上一版本
    git reset --hard HEAD^
    git reset --hard HEAD~2 回到前2个提交
    git reset --hard commit_id

    git reflog  显示的是操作日志（全部）
    git log 不能显示 回退完之后（回退版本之前的） 日志 
```

#### checkout
```
    git checkout -- test.txt  修改的是工作区（相对于最后一次添加到暂存区的内容）
    git reset HEAD test.txt  从暂存区移到工作区
    git branch -m master new 分支改名为new 

    git stash 临时保存
    git stash list
    git stash pop 将临时保存的恢复过来，
    git stash apply

```

#### 标签与diff
```
    git tag v1.0
    git tag -a v1.1 -m "1.1版本"

    git blame 文件名  ： 查看文件都是谁修改的能够定位到 

    git diff  比较的是暂存区与工作区
    git diff --cached commit_id  暂存区与提交区的比较
    git diff HEAD 工作区与commit版本库最新的比较
```

#### pull、push
```
    push 推送
    pull 拉取、同时会执行合并merge
    pull = fetch + merge

    git remote add origin git@github.com:zhu6688/tt.git
    git push -u origin master   -u 只的是本地的master 与 远程的做关联
    下次提交 就直接  git push 

    git remote show   显示所有远程仓库别名（代表地址）
    git remote show origin 显示远程仓库的信息

    一般3套环境：
    1. 开发分支 develop  频繁变化
    2. 测试环境分支 test  供测试与产品等人使用的分支，变化不是特别频繁
    3. master  生产发部分支  （不变）
    4. bugfix 分支  生产系统当中出现bug，用于紧急修复的分支 

    ssh-keygen  生成公钥

    git branch -a 查看远程分支
    git branch -av 查看远程分支会显示最后一次提交信息

    git clone  xxx  name2 : 这是克隆项目以name 为目录的名字    
```

#### 设置别名、分支
```
    git config --global alias.br branch  用br  代替branch
    拉取远程分支 git pull 拉取完成之后，本地没有这个分支，通过下面的操作创建本地的分支并关联上
    git checkout -b develop origin/develop // 在本地创建分支并关联远程的develop分支
    或者
    git checkout --track origin/develop
    删除远程分支：
    git push origin :develop   把本地的空的分支推送到远程的develop 就是删除远程的分支
    git push origin --delete develop 
    远程创建与本地分支不一样的名字
    git push --set-upstream origin dev:dev2
    git push origin dev（源）:dev2（远程的）  将本地的推送到远程的dev2， 这是最完整的写法
```
#### 标签
```
    创建
    git tag v1.0 -m "v1.0标签名"
    查看
    git show v1.0
    搜索
    git tag -l "*.0"
    推送到远程
    git push origin v1.0 单个推送
    git push origin --tags 全部推送
    删除远程的标签
    git push origin :refs/tags/v1.0 
    或者
    git push origin --delete tag v1.0 
```


#### 常用命令
| 版本管理    | 查看信息    | 远程协作 |
| :-         | :-          | :-:     |
| git add    | git help    | git pull|
| git commit | git log     | git push|
| git rm     |  git diff   | 




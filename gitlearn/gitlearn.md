# 1git初始化

```sh
//显示版本库目录所在的位置
git rev-parse --git-dir
//显示工作区根目录
git rev-parse --show-toplevel
//相对于工作区根目录的相对目录
git rev-parse --show-prefix
//显示从当前目录（cd）后退（up）到工作区的根的深度
git rev-parse --show-cdup

```

配置文件的区别
```sh
//在工作区根目录下
//版本库级别的配置文件.git/config
git config -e 
//全局配置文件/home/用户名/.gitconfig
git config -e --global
//系统级配置文件/etc/gitconfig
git config -e --system
```

```sh
//读取配置文件的内容
git config core.bare
//修改配置文件属性值
git config a.b something
```

# 2git暂存区
```sh
//查看提交日志 --stat参数查看每次提交的文件变更统计
git log --stat
//查看工作区和提交缓存区之间的差异
git diff
//查看工作区和版本库之间的差异
git diff HEAD/git diff master
//查看提交缓存区和版本库之间的差距
git diff --cached 
//更新暂存区的目录树，写入修改文件内容到新对象中
git add
//将暂存区目录树写到版本库，更新master分支
git commit
//重写暂存区目录树，被master分支的目录树所替换
git reset HEAD
//从暂存区删除文件，工作区不做改变
git rm --cached <file>
//暂存区全部或指定文件替换工作区文件，危险操作 ，会清楚工作区未添加到暂存区的改动
git checkout . / git checkout -- <file>
//使用HEAD指向的master分支中的全部或者部分文件替换暂存区和以及工作区中的文件,不但会清除工作区中未提交的改动，也会清除暂存区中未提交的改动
git checkout HEAD ./git checkout HEAD <file>
``` 
## 2git diff魔法
```sh
//查看版本库中提交的目录树
git ls-tree -l HEAD
//命令清除当前工作区中没有加入版本库的文件和目录
git clean -fd
//使用暂存区刷新工作区
git checkout . 
//查看暂存区的目录树
git ls-files -s
//需要先将暂存区目录树写入对象库,然后根据写入的tree返回的hashID
git write-tree
git ls-tree
//对本地所有执行变更的文件执行提交操作，建议少使用
git commit -a

```

## 3git对象
### git对象库探秘

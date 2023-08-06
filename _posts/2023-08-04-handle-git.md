HANDLE GIT

system: ubuntu20.04

work address: **310ubuntu:/home/ubuntu/fdisk_d/JiangXiaotian/Handle_Git**

# 0.quike view

```shell
#record
git config user.name "cytosineXT"
git config user.email "cytosinext@gmail.com"

git init #创建git仓库(初始化)
git add readme.txt #添加新文件、新修改到暂存区					gitlens:暂存更改"+"
git commit -m "xxx is xxx" #提交新文件、新修改到本地仓库		     gitlengs:提交更改"√"

git status #查看当前缓存区状态
git diff readme.txt #查看readme.txt的(save但未add的)修改
git diff HEAD -- readme.txt #查看工作区HEAD和版本库readme.txt的区别
git log #print完整log
git log --pretty=oneline #print精简log
git reflog #记录每一次命令和对应commit id

git reset --hard HEAD^ #回滚上一版本
git reset --hard 47d0 #用commit id回到任意版本
git reset HEAD readme.txt #unstage 将暂存区的更改撤销(直接删除)
git checkout -- readme.txt #放弃工作区的修改，回退到stage或repository的版本(用版本库里的版本替换工作区的版本)
git rm readme.txt #删除文件并放入Stage(等价于在文件夹内删除后add)

git branch pdpd #创建新pdpd分支
git switch pdpd #切换到pdpd分支
git switch -c dev #创建并切换到新dev分支
git branch #查看分支
git merge dev #合并指定dev分支到当前分支
git merge --no-ff -m "merge with no-ff" dev #合并指定dev分支到当前分支并禁用快速合并(需要提交commit，会留下合并信息)
git branch -d dev #删除分支(无法删除未合并的有改动的分支)
git branch -D dev #强行删除分支

git stash #缓存工作区，可以缓存多个
git stash list #查看stash缓存的工作现场
git stash apply #恢复缓存区(最新)内容
git stash drop #删除缓存区(最新)内容
git stash pop #恢复并删除缓存区(最新)内容
git stash pop stash@{0} #恢复并删除指定的stash@{0}版内容

git cherry-pick <commit> #复制特定commit到当前分支(改过的bug不用再改一遍，同时此操作会形成一个新的commit)
```

![image-20230804202723367](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230804202723367.png)

```shell
HEAD #当前版本
HEAD^ #上一个版本
HEAD^^ #上两个版本
HEAD~100 #上100个版本
```

```shell
git aliases #为指令创建别名
git config --global alias.logg 'log --graph --oneline'  # 创建 "logg" 别名来代替 "log --graph --oneline"
git config --global alias.gst 'git '
```



# I. follow liaoxuefeng.com's guide

## 1.initialize

```shell
mkdir Handle_Git #创建目录
cd Handle_Git
pwd #显示当前文件夹
```

> /home/ubuntu/fdisk_d/JiangXiaotian/Handle_Git

```shell
git init #把这个目录初始化为git repository, .git是跟踪管理版本库的
```

> Initialized empty Git repository in /home/ubuntu/fdisk_d/JiangXiaotian/Handle_Git/.git/

now, the initialization of the git repository is done.

![](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230804163824298.png)

On the other hand, there are 3 files in the folder now that I just created.

## 2.add and commit file/modify

```shell
git add readme.txt #将文件从工作区添加到暂存区
git commit -m "create a readme file" #将暂存区文件提交到仓库，一次会提交所有已add到repository的files
```

> [master (root-commit) 1a95505] create a readme file
>  1 file changed, 2 insertions(+)
>  create mode 100644 readme.txt

modify the readme.txt and then

![image-20230804170911228](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230804170911228.png)

```shell
git add trytry.py trytry2.py
git status #查看repository状态
```

> On branch master
> Changes to be committed:
>   (use "git restore --staged <file>..." to unstage)
>         new file:   trytry.py
>         new file:   trytry2.py
>
> Changes not staged for commit:
>   (use "git add <file>..." to update what will be committed)
>   (use "git restore <file>..." to discard changes in working directory)
>         modified:   readme.txt

```shell
git diff readme.txt #查看readme.txt的修改
```

> diff --git a/readme.txt b/readme.txt
> index 629f6b7..be836b4 100644
> --- a/readme.txt
> +++ b/readme.txt
> @@ -1,2 +1,2 @@
> -Git is a version control system
> +Git is a distributed version control system
>  Git is free software
> \ No newline at end of file

```shell
git add readme.txt #提交修改到暂存区
git commit -m "add distributed and 2trytry" #提交修改和新文件到本地仓库
```

> [master b0f15c9] add distributed and 2trytry
>  3 files changed, 1 insertion(+), 1 deletion(-)
>  create mode 100644 trytry.py
>  create mode 100644 trytry2.py

```shell
git status
```

> On branch master
> nothing to commit, working tree clean

## 3.reroll

modify it again and then

```shell
git add readme.txt
git commit -m "add GPL"
```

> [master 5e6b1a4] add GPL
>  1 file changed, 1 insertion(+), 1 deletion(-)

```shell
git log #查看日志(历史记录)
```

> commit 47d00efa7c26faa263128ec1da9c1c05653f83aa (HEAD -> master)
> Author: cytosineXT <cytosinext@gmail.com>
> Date:   Fri Aug 4 17:38:35 2023 +0800
>
>     new name and email
>
> commit 5e6b1a40b3ea9e693763e496bc4967e26ef677ed
> Author: albert_wei <auroua@yeah.net>
> Date:   Fri Aug 4 17:30:23 2023 +0800
>
>     add GPL
>
> commit b0f15c988c56fe16b130c9474c987d894a4c854b
> Author: albert_wei <auroua@yeah.net>
> Date:   Fri Aug 4 17:16:25 2023 +0800
>
>     add distributed and 2trytry
>
> commit 1a95505a59bfc065820412e7ed9ce68e0a24b17d
> Author: albert_wei <auroua@yeah.net>
> Date:   Fri Aug 4 16:44:38 2023 +0800
>
>     create a readme file

```shell
git log --pretty=oneline #查看精简日志
```

> 47d00efa7c26faa263128ec1da9c1c05653f83aa (HEAD -> master) new name and email
> 5e6b1a40b3ea9e693763e496bc4967e26ef677ed add GPL
> b0f15c988c56fe16b130c9474c987d894a4c854b add distributed and 2trytry
> 1a95505a59bfc065820412e7ed9ce68e0a24b17d create a readme file

```shell
git reset --hard HEAD^
```

> HEAD is now at 5e6b1a4 add GPL

![image-20230804195029185](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230804195029185.png)

```shell
git reset --hard HEAD^
```

> HEAD is now at b0f15c9 add distributed and 2trytry

![image-20230804195057499](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230804195057499.png)

```shell
git reset --hard 47d0 #用commit id(只要前几位就行，git会自动去找)重返未来
```

> HEAD is now at 47d00ef new name and email

![image-20230804195344018](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230804195344018.png)

## 4.status

![image-20230804203505915](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230804203505915.png)

firstly, when ==Working Directory== has no modify, status will print "clean"

> On branch master
> nothing to commit, working tree clean

if we modify the txt in the upside of the screenshot and save, status will print (have not added)

> On branch master
> Changes not staged for commit:
>   (use "git add <file>..." to update what will be committed)
>   (use "git restore <file>..." to discard changes in working directory)
>         modified:   readme.txt
>
> no changes added to commit (use "git add" and/or "git commit -a")

​		(and the "modified:   readme.txt" is in red)

if add the modify to ==Stage==, status will print (have not commit)

> On branch master
> Changes to be committed:
>   (use "git restore --staged <file>..." to unstage)
>         modified:   readme.txt

​		(and the "modified:   readme.txt" is in green)

if commit the modify to ==Repository==, status will print as initial, because the ==Working Directory== is clean now again

> On branch master
> nothing to commit, working tree clean

## 5.manage the modify

![image-20230804202723367](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230804202723367.png)

Git chase the modify (not the file). 

- When the modify is **save**d it is on the ==Working Directory==, and Git will recognize the modify (in red words) but not record it.
- Then when the modify is **add**ed, it is on the ==Stage==. and Git will also recognize the modify (in green words) but nor record it.
- Last but not the least, when the modify is **commit**ed, it is on the ==Repository==, and now Git will record it by **reset** (distribute a "commit id" as it's version id), and can reroall any version at any time, as long as we know the id.

undo the modify:

```shell
git checkout -- readme.txt
```

when the modify in ==Working Directory==, this command will check the corresponding content in ==Stage== or ==Repository== (when the ==Stage== is empty) and undo the modify using the old content.

For example, now the readme.txt at ==Repository== has content as follow:

![](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230805150851963.png)![image-20230805150321679](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230805150321679.png)(!!!)

![](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230805150538008.png)![image-20230805150410902](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230805150410902.png)(!!!??)

after i modify it, the "更改" region will show it, indicate the ==Working Directory== content is different from the ==Stage== or the ==Repository== one.

![image-20230805151746601](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230805151746601.png)(!!!??)

![image-20230805151839365](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230805151839365.png)(!!!??!!)

add it to ==Stage==, and then modify it again, now we have 3 version of content, so as (!!!) (!!!??) (!!!??!!) that in ==Repository== ==Stage== and ==Working Directory== saperately. 



if i want to use the version in ==Stage==:

```shell
git checkout -- readme.txt
```

now![image-20230805152313408](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230805152313408.png)(!!!??)

elif i want to use the version in ==Repository==, i can abandon the ==Stage== then **checkout**, or  **reset** derectly.

```shell
git reset HEAD readme.txt
```

​	abandon the stage![image-20230805152809516](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230805152809516.png)(!!!??!!)

```shell
git checkout -- readme.txt
```

​	then checkout![image-20230805152849194](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230805152849194.png)(!!!)



or

```shell
git reset --hard HEAD
```

​	reset derectly![image-20230805153002889](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230805153002889.png)(!!!)

now the figure will change:

![image-20230805154439219](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230805154439219.png)

![image-20230805164548007](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230805164548007.png)

## 6.branch

create and switch

```shell
git branch pdpd #创建新pdpd分支
git switch pdpd #切换到pdpd分支
git switch -c dev #创建并切换到新dev分支

git branch #查看分支
git merge dev #合并指定dev分支到当前分支
git merge --no-ff -m "merge with no-ff" dev #合并指定dev分支到当前分支并禁用快速合并(需要提交commit，会留下合并信息)
git branch -d dev #删除分支
```

handle conflict

```shell
git switch -c featurel
git switch master
git merge featurel
```

change the last 2 row, create a conflict, then 

![image-20230806124952995](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230806124952995.png)

![image-20230806125649428](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230806125649428.png)

when in conflict, the vs coder will go into the mergeing mode. After i decide the modify chosen and commit the decition (or new modify), the branches will merge.

```shell
git log --graph --pretty=oneline --abbrev-commit #查看分支合并情况
```

![image-20230806130200142](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230806130200142.png)

  view the changes in oneline.

## 7.stash store working area

when the working area (==Working Directory==+==Stage==) have modify, u can't switch the branch. storeing the woking area temporally  is a wise choice.

![image-20230806144011753](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230806144011753.png)

![image-20230806144105413](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230806144105413.png)

```shell
git stash #缓存工作区
```

![image-20230806144233404](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230806144233404.png)

u see, the modify in ==working directory== is disappeared, and the git status is clean.

```shell
git stash list #查看stash缓存的工作现场
git stash apply #恢复缓存区(最新)内容
git stash drop #删除缓存区(最新)内容
git stash pop #恢复并删除缓存区(最新)内容
git stash pop stash@{0} #恢复并删除指定的stash@{0}版内容
```

![image-20230806150226773](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230806150226773.png)

## 8.commit tag

use tag to replace the complex and confucious commit id, on the recent branch

```shell
git tag v1.0 #对当前branch当前commit打上"v1.0"的tag
git tag #查看所有标签
git tag v0.9 <commit> #对指定commit打上"v0.9"的tag
git show v0.9 #查看tag的信息
git tag -a v0.1 -m "version 0.1 released" <commit> #创建带有说明的标签，-a标签名 -m说明
```

now u can use the tag to address the specific commit.

## 9.remote and online

waiting for later...










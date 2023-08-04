HANDLE GIT

system: ubuntu20.04

work address: **310ubuntu:/home/ubuntu/fdisk_d/JiangXiaotian/Handle_Git**

```shell
#record
git config user.name "cytosineXT"
git config user.email "cytosinext@gmail.com"

git init #创建git仓库(初始化)
git add xx.py #添加新文件、新修改到暂存区
git commit -m "xxx is xxx" #提交新文件、新修改到本地仓库

git status #查看当前缓存区状态
git diff xx.py #查看xx.py的(未保存的)修改
git log #print完整log
git log --pretty=oneline #print精简log
git reflog #记录每一次命令和对应commit id

git reset --hard HEAD^ #回滚上一版本
git reset --hard 47d0 #用commit id回到任意版本
```

![image-20230804202723367](https://raw.githubusercontent.com/cytosineXT/PicGoimgbed/main/images/image-20230804202723367.png)

```shell
HEAD #当前版本
HEAD^ #上一个版本
HEAD^^ #上两个版本
HEAD~100 #上100个版本
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

![image-20230804163824298](C:\Users\cytosineXT_LLab\AppData\Roaming\Typora\typora-user-images\image-20230804163824298.png)

On the other hand, there are 3 files in the folder now that I just created.

## 2.add and commit file/modify

```shell
git add readme.txt #将文件添加到暂存区
git commit -m "create a readme file" #将暂存区文件提交到resository，一次会提交所有已add到repository的files
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

等明天学，先下班。
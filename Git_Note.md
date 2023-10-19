# Git&Github学习

## 1.Git入门

### 1.1初步使用

```
git init 初始化

git status 检测当前文件夹文件状态

git add 文件名 管理文件

git add . 管理所有文件

git commit -m '版本描述'

git log 查看版本记录

git reflog 查看历史版本记录

git log --graph  以图标方式展示版本记录

git log --graph --pretty=format:"%h %s"  简洁方式显示版本记录

git reset --hard 版本号 回到某个版本
```

### 1.2 分支

#### 1. 创建分支

```
分支作用：环境隔离

git branch 查看分支

git brach 分支名  创建分支

git checkout 分支名  切换到分支
```

#### 2.合并分支

```
1. 切换回master分支（主分支）
	git checkout master
	
2.合并分支
	git merge 要合并的分支名

3.删除合并过的分支（无用的分支）
	git branch -d 分支名
	
4.问题：分支合并的相同的内容有冲突，手动修改代码

		然后 git status 
		git add 文件名
		git commit -m '版本描述'
```

![image-20230127143453006](C:\Users\33897\AppData\Roaming\Typora\typora-user-images\image-20230127143453006.png)



## 2. Github

#### 1. 推送文件

```
1. 给远程仓库起别名
git remote add origin(自定义名字) 远程仓库地址（GitHub仓库地址）

2.向远程推送代码
git push -u origin 分支名	（推送一个分支的文件）
```

#### 2. 下载仓库文件

```
1.克隆
	git clone 远程仓库地址（内部已实现git remote add origin 远程仓库地址
2.切换分支
	git checkout 分支名
```

```
git pull origin dev  从远程仓库直接拉文件到本地工作区

git fetch origin dev
git merge origin/dev
```

## 3. 问题

### 3.1 Git 报错 Updates were rejected because the remote [contains](https://so.csdn.net/so/search?q=contains&spm=1001.2101.3001.7020) work that you do

Git 报错 Updates were rejected because the remote contains work that you do
这个报错实在是让我受不了了，每次不管是‘命令行’ 还是 idea 提交都会出现这样让人心态爆炸的问题。然而每次出现又重复的查找解决办法，这次实在受不了了，便有了这篇文章，希望它也能帮助到心态爆炸的你。

1、命令行出现这种情况
命令行执行会出现这样的问题是因为错误的提交过程：

git init //初始化仓库
git add .(文件name)                  //添加文件到本地暂存
git commit -m “first commit”        //添加文件描述信息
git remote add origin    远程仓库地址 //链接远程仓库
git push -u origin master          //把本地仓库的文件推送到远程仓master                                      分支

这样就出现了标题提示的错误信息，如下图：

![image-20210604105941769](https://img-blog.csdnimg.cn/img_convert/634bfdb46101faca5327d62c2507170f.png)

经过多次出现同样的问题，我已经对这个问题的原因了如指掌了，这是因为在本地新建库后，与远程仓库的内容不一致导致的（远程仓库有一些内容本地没有）。问题了如指掌，但是解决方法每次都记错，所以还是记录一下吧。

正确的提交过程如下：

git init                           //初始化仓库
git add .(文件name)                //添加文件到本地 
git commit -m “first commit”      //添加文件描述信息
git remote add origin  远程仓库地址 //链接远程仓库 
git pull origin master           // 把本地仓库的变化连接到远程仓库master分支
git push -u origin master        //把本地仓库的文件推送到远程仓库master分支

在执行上面第五步的时候可能会出现新的错误，也是常见的错误了，错误信息如下：

![image-20210604110514047](https://img-blog.csdnimg.cn/img_convert/1fd57c5313639c3ac44d8ebfe829bde2.png)

不要慌，这是因为文件版本没有及时更新，两个分支是两个不同的版本，具有不同的提交历史，决绝方式就是在原本的命令之后加上一句命令即可：

git pull origin master --allow-unrelated-histories

然后有的情况下，输入上面的命令就能解决问题，有的情况下，他又会报新的错误，如下：

![image-20210604110855717](https://img-blog.csdnimg.cn/img_convert/2734e6825e41a98c894f2ef308b381af.png)

网上查了解决办法是真的麻烦，但是原因知道了，就是有文件冲突，没有更新，那就好办了，重新输入以下命令问题解决：

![image-20210604111243288](https://img-blog.csdnimg.cn/img_convert/ff117dae89b993d1acdbcd8ae133ef3f.png)

2、idea出现同样的报错，解决方式同上
输入命令的地方在 idea 的下方，有一个 terminal ，点击之后，即可输入上面的命令。
————————————————
版权声明：本文为CSDN博主「很萌の萌新」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/liulei952413829/article/details/117553977


因为有两台笔记本，我想在这两台笔记本上写一点笔记，所以就想到了使用git来实现，不仅可以防止我写的东西丢掉，还省去了我要传东西的时间（就是访问github的时候有点不稳定，还有对git的一些使用并不是很熟悉），这个文件用来记录我在使用的过程中，使用到了哪些git方面的东西，因为啥也不懂，所以很多都是现查现用的，怕这些东西忘记，所以记录一下



在当前文件下初始化.git文件（第一件要做的事）

```
git init
```

 这几个命令按顺序执行，用来保存一个文件的更改

```
git add 文件名.文件类型（也可以是目录名）
git commit -m "提交描述"
// 连接远程仓库
git remote add origin https://github.com/用户名/仓库名
（在做这一步的时候我将origin拼错了，后来导致了一些错误，英语还是要学号
	这是修改错误的代码
		git remote -v // 用来查看远程仓库详细信息，可以看到仓库名称
		git remote remove orign // 删除错误仓库名称
		git remote add orign 仓库地址 // 重新连接仓库
）
git push origin master
```

使用另外一台电脑进行开发

```
git pull https://github.com/用户名/仓库名 分支名
// 这样就可以将GitHub上的文件copy下来，提交更改的方法和上面一样
```

删除文件及文件夹

```
git rm 文件
git rm -r 文件夹（可以删除有内容的文件夹）
```
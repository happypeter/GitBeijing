---
title: 简单分支操作
---

今天的主角是分支，因为不介绍分支（ branch ）的概念，下面的操作是没办法介绍了。可以这样说，Git 最核心的操作对象是版本（ commit ），最核心的操作技巧就是分支。

## 什么是分支？

仓库创建后，一旦有了新 commit，默认就会放到一个分支上，名字叫 master。前面咱们一直看到的多个版本组成的一条历史线，就是 master 分支。但是一个仓库内，用户可以自己创建其他的分支，可以有多条历史线。

说说 master 这个名字，一般中文叫“主分支”，其实从技术底层来讲它跟其他我们自己要创建的分支没有区别，只不过它是天生的默认分支。实际工程项目中会人为的给它一个重要的使命，存放稳定代码。就像 github 公司[倡导](http://scottchacon.com/2011/08/31/github-flow.html)的。

> master 分支上的所有代码都应该是可以部署的

意思就是 master 分支上的代码是通过了测试的，可以随时放心的放到产品服务器上跑的代码。这样，如果想开发一个新功能，可以新开分支。想象一下历史线上有很多节，每个版本就是一节。一个分支相当于一跟竹子，一节节的往上长。

![](https://happypeter.github.io/images/2019031501.jpg)

但是实际上在底层并不是每个分支都拷贝出自己独立的一条历史线。其实 master 本身只是一个指针，指向 master 分支上最新的一个版本。这样由于每个 commit 都可以找到自己的前一个 commit，那么这条历史线就可以确定了。

![](https://happypeter.github.io/images/2019031502.jpg)


## 创建新分支

什么时候需要开一个新分支，这个后面讲各种工作流程的时候会介绍，今天先把基本操作学会。单击界面顶部的分支名，就可以显示所有分支。

![](https://happypeter.github.io/images/2019031503.jpg)

如果想创建一个新分支，只需要点 `new branch` 按钮。

![](https://happypeter.github.io/images/2019031902.jpg)

弹出的界面中可以看到

> Your new branch will be based on your currently checked out branch(master)

意思是

> 你的新分支会基于你的当前分支（ master ）.

或者说白了就是，新分支 idea 会跟 master 有完全一样的历史。

![](https://happypeter.github.io/images/2019031505.jpg)


可以看到新的 idea 分支下，项目历史线果然跟 master 分支一模一样。但是，在底层这个的实现是非常巧妙的，就是又创建一个新的 idea 指针，跟 master 指针指向同一个版本，根本没有拷贝历史线。

![](https://happypeter.github.io/images/2019031506.jpg)

如果现在我对项目做一下修改，然后 commit 了。那么移动的只是 idea 指针，master 不变。就成了这样：

![](https://happypeter.github.io/images/2019031507.jpg)

现在 master 分支包含两个版本 C1 和 C2，idea 分支包含三个版本 C1，C2，C3 。

默认情况下这个 idea 分支只是存在于本地，如果想在远端仓库上发布这个分支，就点一下 idea 分支右侧的 `Publish Branch` 按钮。

这样，到远端仓库看一下，发现果然多了一个 idea 分支，搜索框中，不但能搜索已有分支，还能创建新分支，看到了吧，很多操作在本地客户端和 github.com 上都能进行。

![](https://happypeter.github.io/images/2019031508.jpg)

这就是创建新分支的原理和具体操作方式了。

## 切换分支

下面来看如何在各个分支之间做切换。

点 current branches 标签，就可以显示所有分支，想要切换到哪个分支，点一下就切换过去了。时间长了你会觉得这个也不够快，还是纯键盘操作快。敲 Cmd-B 可以打开分支切换框，输入名字回车，就切换成功了。

![](https://happypeter.github.io/images/2019031509.jpg)

每次切换分支的时候，其实也是底层有一个名为 HEAD 的指针在不断发生变化，比如当然 HEAD 指向 master ，那么 master 就是当前分支。

![](https://happypeter.github.io/images/2019031510.jpg)

注意，每次切换分支，项目代码，术语叫工作树（ Working Tree ）是会随着变化的，在编辑器中看看就知道了。

这样，我们就学会了如何去切换分支。至于如何去删除一个分支，当前版本的客户端中没有这个功能，需要用命令行去操作，这里我们暂时不去介绍。

## 总结

只开测试分支，调好代码 commit 了之后，如果不把代码融合到 master 分支上是没有太大意义的，这就涉及到分支合并的问题了，这个是 git 最大最强的一块功能，后面介绍。

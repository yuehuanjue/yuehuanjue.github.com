---  
layout: article
title:  在Ubuntu14.04上搭建jekyll环境
category: [jekyll]
description: 在Ubuntu14.04上搭建一个jekyll环境.为了可以及时的将自己的一些笔记及时的更新到github,而做的准备.    
tags: [github, jekyll]
keywords: [github, jekyll]
updateData:   13:42 2017/05/02
---

## 前言

时隔五个月,又一次的开始写博客了. 在这五个月里, 真是变化万千,但是作为一个程序猿,我们还是离不开的努力和脚踏实地.  

古人常说,工欲善其事,必先利其器. 本着"利其器"的原则,  在现在的Ubuntu14.04的环境下, 搭建jekyll, 以便于随时更新一些学习笔记. 

然而,不用不知道,原来有那么多的坑,  好吧, 现在就来聊聊踩过的坑. 


## 搭建步骤:

像我这种使用Python完成项目的,只知其然,不知道其所以热的程序猿, 会经常使用ubuntu 系统, 为我们提供的apt-get指令, 曾一度认为, 在Ubuntu下, 搭建环境,就没有apt-get安装不好的, 然而我也将因为自己的幼稚的想法,而付出代价.  

```
sudo apt-get install jekyll
```

当然, 用这个方法安装jekyll, 一般安装是没有问题的, 如果你遇到了问题, 就请自行Google吧,  这种概率实在是小. 但是安装好,不一定就可以使用了, 我们要去项目中,用jekyll server 跑一下看看.   如果你一次成功,那么恭喜你, 不用看下去了; 如果没成, 那么ok, 这是我们现在要讨论的部分. 

不知道,大家遇到的都是什么问题,  简单说一下我遇到的问题.
```
/usr/lib/ruby/1.9.1/rubygems/custom_require.rb:36:in `require': cannot load such file
```
从路径上可以看出来的是, 使用apt-get 安装的jekyll, 默认使用的是/usr/lib/ruby的版本,  这个是系统自带的ruby.(在这里简单说一下, 使用jekyll, 要基于ruby的, 一般使用gem去安装的).
因为ruby版本的问题,  而产生的错误,  目前使用apt-get是解决不了的, 因为版本库里的ruby就到1.9.3版了,  貌似有一种不想升级的架势.  

so, 这里来提供另外一种解决方式.

方法是使用rvm(试过这个方法不行的朋友,可以拐弯返航了)

1, 使用 rvm -v 看一下系统有没有安装rvm
```
rvm 1.29.1 (latest) by Michal Papis, Piotr Kuczynski, Wayne E. Seguin [https://rvm.io/]
```

2, 安装完rvm后, 使用rvm install 2.4, 来安装ruby.  这里要说的是,  我很好奇, 为什么只用版本号就默认的是安装ruby了啊,   猜想rvm是ruby的专属安装工具.

这里可能没有那么顺利安装好,
更新过系统的朋友, 可能会遇到下面这个问题,

```
hoo@ubuntu:~/yuehuanjue.github.io$ rvm install 2.4
......
下列信息可能会对解决问题有所帮助：

下列软件包有未满足的依赖关系：
 libffi-dev : 依赖: libffi6 (= 3.1~rc1+r3.0.13-12) 但是 3.1~rc1+r3.0.13-12ubuntu0.1 正要被安装
E: 无法修正错误，因为您要求某些软件包保持现状，就是它们破坏了软件包间的依赖关系。
++ return 100
++ return 100
Requirements installation failed with status: 100.
```
意思就是, libffi6的版本过高, 需要一个低版本的.

解决方案是;使用aptitude来调整,  用sudo apt-get install aptitude来安装, 使用是sudo aptitude install libffi-dev

```
....
下列软件包存在未满足的依赖关系：
 libffi-dev : 依赖: libffi6 (= 3.1~rc1+r3.0.13-12) 但是 3.1~rc1+r3.0.13-12ubuntu0.1 已安装。
下列动作将解决这些依赖关系：

     保持 下列软件包于其当前版本：
1)     libffi-dev [未安装的]      


是否接受该解决方案？[Y/n/q/?] n
下列动作将解决这些依赖关系：

     降级 下列软件包：                                                           
1)     libffi6 [3.1~rc1+r3.0.13-12ubuntu0.1 (now) -> 3.1~rc1+r3.0.13-12 (trusty)]



是否接受该解决方案？[Y/n/q/?] y
下列软件包将被“降级”：
  libffi6 
.....

```
这里很明显看到,aptitude会为我们提供各种解决方案.

那么下面就好说了,  安装 rvm install 2.4 (pass)
使用2.4版本的ruby:  rvm use 2.4  
安装jekyll: gem install jekyll

安装好jekyll后, 我们jekyll server时, 会有个小错:
```
/home/hoo/.rvm/rubies/ruby-2.4.0/lib/ruby/2.4.0/rubygems/core_ext/kernel_require.rb:55:in `require': cannot load such file -- bundler (LoadError)
```
那么 我们需要 安装bundler: gem install bundler
安装好bundler后, 需要安装一下依赖:bundle install 
此后 jekyll  server 可以正常使用啦.
当然, 如果最后几步还有其他问题, 可以参考一下其他文章,  这里就不再重复了.  如果其他文章也没有解决, 那就是我还没有遇到过的情况了, 可以留言,我会亲自实验一下,找出正解.

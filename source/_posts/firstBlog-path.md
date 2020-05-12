---
title: 记录Gitee+Hexo搭建博客主题样式及图片不显示问题
date: 2020-02-08 22:12:45
tags:  [Blogs,Gitee]
categories: 学习
---
## 主题样式及图片不显示问题
使用**Git+Hexo+GitHub/Gitee搭建个人博客**的详细准确教程网上有很多，本人也是按照网上大佬们的教程进行操作的，这里不再重复，本文主要记录一下在搭建个人博客时遇到的几点问题，供已经了解搭建流程并存在类似问题的同学阅读交流。

首先是搭建基于Git+Hexo+GitHub的个人博客，基本没什么问题就实现了，但实现后发现个人博客网页刷新实在是慢。于是选择Gitee（码云）建仓库搭建博客，然而遇到了一些路径问题，问题一解决比较简单，此处略作记录；问题二鲜少有提及，此处仅针对我尝试并成功的修改做说明。
<!--more-->

### P1：本地（localhost:4000）显示正确但上传到Gitee后主题样式不显示
此时显示如下图所示，因为这是后来测试时截的图，图片路径已设置好，故此时图片显示正确，但样式无法显示：
![不显示主题样式](1.png "不显示主题样式")
在所建博客本地仓库目录下的_config.yml文件中如下位置做出如下修改：
![root路径修改](2.png "root路径修改")
按照注释中修改如下：
![url及root路径修改](3.png "url及root路径修改")  
##### Ps:在搜索与尝试过程中发现，仅修改root路径也可使样式正确显示，url可以不做修改。

### P2：主题样式成功显示，但上传到Gitee后主题图片不显示
经过修改root路径后，样式可以成功显示，但又发现主题图片无法显示，此时主页刷新（多刷新几次）显示如下图所示：
![不显示主题图片](4.png "不显示主题图片")
查看源代码，看到图片位置显示alt内容能够想到应该是图片路径问题，在主题路径下的_config.yml文件内修改图片路径，经过多次尝试更改路径，图标、Logo及Cover路径改为相对路径即images/favicon.ico、images/ayer-side.svg和images/cover4.jpg时能够成功显示主页图片及侧边栏Logo，但网页标题图片无法显示且当导航到其他页面时，侧边栏Logo仍无法正常显示：
![不显示网页标题图标](5.png)
![不显示侧边栏Logo](6.png)
修改主要注意以下两点：1、将图片相对路径改为绝对路径；2、此处绝对路径为Gitee上个人博客远程仓库上的绝对路径。
![修改图片绝对路径](7.png)
修改后博客页面即可正常显示:
![博客页面正常显示](8.png)
在GitHub上完全没有遇到以上路径问题，而且看其他大佬教程中也没有提到这个问题，应该跟我Gitee Pages生成的网站地址有关，比别人多了 **/lynn_blog**。
![博客页面正常显示](10.png)

### P3：fatal: not a git repository (or not any parent up to mount point /mnt)
新搭建的博客在仓库主页没有README.md文件，想要新增一个README.md文件，结果在输入git add README.md命令时报错：fatal: not a git repository (or not any parent up to mount point /mnt)。
首先进入你新建博客目录下的.deploy_git目录中，添加README.md文件，输入命令$ echo "#Lynn_Blog" >> README.md（该命令可不在.deploy_git目录下进行）和$ git add README.md（该命令必须在.deploy_git目录下进行，否则报错）也不会报错，原因是为与远程仓库连接的是.deploy_git目录。
![正确路径演示](9.png)

#### 如大家仍有问题或遇到其他问题，欢迎一起交流学习！




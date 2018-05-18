---
layout:     post
title:      "Python入门————包管理工具"
subtitle:   "Python包管理工具pip和Anaconda的作用"
date:       2018-05-18 15:32:00
author:     "SethD"
header-img: "img/post-bg-dubai.jpg"
tags:
    - Python
    - 包管理
	- Anaconda
---

> 为什么需要使用pip
  Python和Java等语言一样有着许多可以被引用的库，丰富的库提供了很多方便的变量和方法供使用者直接使用，降低了编程的复杂度；使用者可以根据业务需要去调用合适的库。
  ```Python
	import sys as args
	```
	例如以上代码块中，import导入了名为“sys”的库，使用了变量’args‘,当然此处的sys库是Python自带的，所以在调用时不会出现问题，但当我们在首次安装Python而且未安装对应的包之前，导包就会出现No module named '**'的错误信息。
	这就是没有导包导致的（由于仓库中找不到对应的包）。
	而pip就是一种Python包管理工具。


> pip的功能
	正如上面所说，pip是用来导包的，即将Python库按照模块的形式导入并安装到本地仓库。
	除此之外它还有查看、删除、更新等操作。


> pip的安装（Windows）
	在Python官网下载的新版的Python安装包已经包含了pip，比如我在官网下载的是Python 3.6.3，其根目录为Python36，在根目录下的Script文件夹包含了pip执行文件。
	可以直接在该目录下运行pip。但为了方便起见，我们可以把pip所在目录配置到系统环境变量Path中，这样就可以直接在CMD控制台中调用pip命令。
	（网上看到了通过easy install命令在Script文件目录下安装pip的方法，好像没什么区别）
		

> 如何使用pip（pip命令）
	完成以上配置之后，就可以直接打开CMD，运行pip命令。
	
	*install
	我们常用的是install命令，用于导入Python包到仓库中。
	例如：
	```
	pip install pandas
	```
	就是导入了pandas库到仓库中。
	（可以看到）
	```
		Installing collected packages: pytz, numpy, six, python-dateutil, pandas
	Successfully installed numpy-1.14.3 pandas-0.23.0 python-dateutil-2.7.3 pytz-201
	8.4 six-1.11.0
	```
	
	*list
	通过 
	```
	pip list
	```
	可以查看到当前仓库中所有的包以及版本号。
	
	*update
	暂时略
	*delete
	暂时略
	
> Anaconda是什么
 Anaconda是常用的一种Python版本及库管理工具
 1、它可以通过创建不同的环境来切换使用不同的Python版本
 2、同时它集成了丰富的常用Python库包
 3、包含了conda，类似于pip的包管理工具，来管理Python包
 *值得注意的是，在Anaconda中，Python和conda都被作为了包/模块来统一管理，这样才造就了它可以随意切换版本环境的特性。

> Anaconda安装
	可以去Anaconda官网去下载安装包，进行安装，安装完成后使用Anaconda Prompt可以直接使用对应命令

>conda命令
	与pip类似，可以通过conda来进行包、模块管理。
	```
	conda install tensorflow
	```
	

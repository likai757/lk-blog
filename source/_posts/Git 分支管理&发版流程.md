---
title: Git 分支管理&发版流程
date: 2016-08-10 19:10:00
categories:
- Git
tags:
- git
---

本文主要介绍 **Git** 版本管理工具在多人协同情况下，出现一些分支的管理混乱问题，现在大部分公司，为了应变市场需求的相应，版本的迭代速度和频率都不断提高，这期间就很容易出现发版与测试管理的混乱，导致生产环境出现一些低级且又严重的错误。
    
-------

### 一、分支管理混乱时，所遇到的问题

1. 发布的版本与测试的版本不一致，***导致生产环境出现不可预期的BUG***；

2. 没有测试的Feature，被合并到Dev分支，***导致Dev分支被冻结，导致其他人从Dev合并代码出现错误***；

3. 没有计划发版的Feature，被合并到Dev分支，***导致产品规划的版本功能，无法被拆解***；


-------

###  二、解决方案GitFlow

这里我们先看一张图：
![GitHub set up](http://likai.me/uploads/git-flow.png)

如图所示：GitFlow是一个已经相对成熟的Git分支管理模型，这里我会先简单介绍一下GitFlow，后面我会针对执行过程中打包测试与发版流程，所遇到的实际问题，规范具体的实施方案。

#### 1. 什么是GitFlow
Git 本身是对项目文件的跟踪与记录，然而git 并没有规定分支的含义，大部分小型或者个人项目，基本只需要master, dev 两个分支就够了，但当项目复杂度提高，人员增多时，dev就会频繁的出现代码冲突，发版功能无法分割的问题。

**GitFlow：**就是给各分支赋予含义，让分支管理变得更加清晰，每个分支有自己的使用场景和主要职责。

<span style="color:#4A90E2">PS：GitFlow的使用，一定要让团队内部人员，对分支的理解达成一致。</span>
#### 2. GitFlow 分支结构
GitFlow 定义了5类基本分支：

* **Production 分支：**也就是我们经常使用的Master分支，这个分支最近发布到生产环境的代码，最近发布的Release， 这个分支只能从其他分支合并，不能在这个分支直接修改

* **Develop 分支：**这个分支是我们是我们的主开发分支，包含所有要发布到下一个Release的代码，这个主要合并与其他分支，比如Feature分支

* **Feature 分支：**这个分支主要是用来开发一个新的功能，一旦开发完成，我们合并回Develop分支进入下一个Release

* **Release分支：**当你需要一个发布一个新Release的时候，我们基于Develop分支创建一个Release分支，完成Release后，我们合并到Master和Develop分支

* **Hotfix分支：**当我们在Production发现新的Bug时候，我们需要创建一个Hotfix, 完成Hotfix后，我们合并回Master和Develop分支，所以Hotfix的改动会进入下一个Release

<span style="color:#4A90E2">PS：在实际应用中可根据项目复杂度简化。</span>

#### 3. GitFlow 发版及测试流程
<span style="color:red">当前Feature开发完成时，将Dev合并到当前Feature分支，在当前分支打包（使用feature命名）；</span>
1、Feature 分支： 

* **打包命名：**feature-[功能名]-[版本号]    （Feature集成测试）
* **使用场景：**添加新的功能模块时创建
* **打包前：**先把Dev合并到当前Feature分支（为了兼容Dev修改可能存在的冲突）
* **测试通过后：**

    * 如果当前Dev与Feature集成测试版本不一致，合回dev分支的版本，需要执行Dev集成测试；
    * 如果当前Dev与Feature集成测试版本一致，合回dev分支的版本，留档存储；
    * <span style="color:red">将当前Feature合并到Dev分支，并在Dev分支重新打包（使用dev命名）；</span>

2、Develop 分支：

* **打包命名：**dev-[版本号]      （Dev集成测试，与Feature集成测试存在差异时执行）
* **使用场景：**
    * 对项目框架，依赖，构建等全局性修改的，直接在Dev上修改。
    * Master分支的Hot Fix修改，需合并到Dev分支。
    * Feature集成测试通过，需合并到Dev分支，打包存档或进行Dev集成测试。
    
* **打包前：**先把Master分支合并到Dev分支（为了兼容HotFix修改可能存在的冲突）
* **测试通过后：**

    * 如果当前Master与Dev集成测试版本不一致，合并Master到Dev分支重新测试。
    * 如果当前Master与Dev集成测试版本一致，合并Dev到Master打包发版。
    * <span style="color:red">将Dev分支合并到Master分支，并在Master分支重新打包（使用release命名）</span>

3、Master 分支：

* **打包命名：**release-[版本号] 
* **使用场景：**

    * 通过Dev集成测试，且要发版上线时，将Dev集成测试通过的版本，合并到Master分支打包发版。
    * 线上有BUG热修复时，创建HotFix分支，修复Bug并合并回Master分支打包发版。

<span style="color:red">PS： 线上发版只能发release</span>
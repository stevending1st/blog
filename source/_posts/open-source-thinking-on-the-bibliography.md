---
title: 开源在现有学科下的思考之古典目录学
sticky: 0
copyright: false
date: 2024-02-21 15:32:58
categories:
- 开源在现有学科下的思考
tags:
- 开源在现有学科下的思考
- 开源
- 目录学
- 开源项目
- 分类
---

**按：** 整理房间，发现笔记中有些东西已经模糊，遂希望将有些思考的东西沉淀下来，备后来回顾。关于开源的一系列思考，没想到决定最先写完的是“开源在现有学科下的思考之古典目录学”，这篇文章源于另一个更大的命题——如何将现有学科与开源结合，这一想法来源于我在读书时的一个体会，每一门课就是一个学科，虽然是不同学科，有些学科之间总有共通的理论，有时甚至相互借鉴。关于这一系列的思考，有过很多组织形式的想法，最后决定每个学科单独写一篇，这样方便更新。在跨领域时，总有人提出“某是在了解甲领域的人中最了解乙领域的人；也是在了解乙领域的人中最了解甲领域的人”云云，但是很可惜，我只能说自己对文章中涉猎的学科都“有些爱好”，甚至可能不能说自己是“爱好者”，当然这些文章可能有幸被了解文中一个或多个领域的方家经眼，如果发现鄙见有缺漏并不吝赐教，实属幸事。

<!-- more -->

## 目录学与开源之关系

古典目录学（如果不特殊说明，后文简称“目录学”）是一门研究古代文献分类、整理和编目方法的学科；开源项目存在大量的分类、整理和编目工作。目录是目和录的合称，篇名或书名为目，对目的说明和编次为录，把一批篇名（或书名）与说明编次到一起即为目录。目录可分为一书目录和群书目录，一本书的篇名与说明编次到一起为一书目录，诸书书名和叙录的总纂被称为群书目录，目录学研究的重点是群书目录，《太史公自序》可被看作《史记》的目录（一书目录），而《四库全书总目》是最要的目录学著作（群书目录）。开源项目目录可以分为一项目目录和群项目目录，一项目目录是单个项目内的文件结构及其说明，这往往涉及软件架构，偏重软件工程化，当然目前也有一些文章从工程化角度在探讨开源项目的文件结构；群项目目录是对多个项目及其说明进行编次，应该是在目录学领域关注的重点。

上面的思考围绕开源项目展开，那么为何不囊括闭源项目？闭源软件因为无法获得源码，无法对其一项目目录进行研究，纯文档类项目内容本身是透明的，与开闭源无关，在讨论群项目目录时，在一定范围内可以囊括闭源软件。所以，在讨论一项目目录时，闭源软件项目往往因为无法获取目录不在讨论之列；在讨论群项目目录时，除了部分涉及源码的内容，大多数情况与开闭源无关。本文的思考主要围绕开源项目展开。

## 开源项目目录的分类

在本文之前，其实已有一些开源项目目录了，这里结合鄙人对开源项目目录的类别思考谈一谈其现状，因为个人见识有限，挂一漏万，希望有幸得到大家的批评指正。

综合目录，是综合诸多项目的目录。目前鄙所知道的我国最大的开源软件目录应该是 OSCHINA 的 [开源软件库][1]，但其中还收录了少量的免费闭源软件如 [GitHub][2]，它提供按语言或功能进行分类，还支持交叉筛选操作系统和语言，此外它的“Awesome 软件”模块提供了一些比较有意思的类部，比如 “[这些游戏模拟器让你重温经典老游戏][3]” ；Gitee 依托开源软件托管在 [开源软件探索页][4] 也展示了不少开源软件，它提供按功能进行分类，还支持按开源许可证和语言进行交叉筛选；另一个比较知名的个人项目是 [HelloGitHub][5]，它的项目比较集中与 GitHub，分类采用标签形式，但在不登录情况下标签比较有限。

专门目录，是专为与某一种专门类别或某一项目有关的开源项目所编的目录。可以分为组织项目目录、子项目目录、某一功能项目目录、某一语言项目目录、项目依赖目录……等等。组织项目目录是某一开源组织罗列的其开源项目的目录，例如 openEuler 社区在 [openEuler/community][8] 仓库的 SIG 组的页面罗列了该 SIG 组的项目清单，比如 [A-Tune][6]。一个较大的开源项目为了较好的开发可能被拆分成多个子开源项目，该较大项目的子项目的目录即为子项目目录，因为 Monorepo 架构的流行，可能使这类项目比较少，这类目录也比较少，比如开源社的 [开放黑客松][7]。某一功能项目目录是围绕某一功能的开源项目的目录，比如上文提到的 [这些游戏模拟器让你重温经典老游戏][3]。某一语言项目目录是围绕某一编程语言的开源项目目录，此类目录常以的 Awesome 项目形式出现（也有相当一部分 Awesome 不是围绕某一编程语言编次的），比如 [awesome-python][9]。项目依赖目录是指罗列某一项目的所有依赖项目的目录，一般通过包管理软件生成。

## 开源项目目录之要素

目录书的基本结构主要包括三个因素：书名、小序和题解（书录）。小序是对某一类部图书的学术流派、演变和特点加以论述。题解主要揭示图书的主旨和用途，向读者指示门径和指示方向。粗略的理解小序是围绕某一类部的说明，而题解是围绕每一部书的说明。借用这些概念，观察现在的开源项目目录，大多数分类清晰，所以不用过多对分类进行解释，少数如前文提到的 [这些游戏模拟器让你重温经典老游戏][3] 会略做说明；综合目录由于项目数量众多，平台只进行审核，所以“题解”的质量往往取决于该项目的提交者或者维护者，大多数专门目录甚至无“题解”或直接复制项目简介，值得注意的是，部分技术选型文章也具备实质性的开源项目目录功能，并且具有较好的“题解”——不仅说明项目的优点，也分析项目的劣势。

## 目录学于开源之功用

“辨章学术，考镜源流”是清代学者章学诚对目录学作用的高度概括。目录学对于开源大体有如下功用：了解开源在各领域的基本状况，便于查阅是否已有成熟的解决方案，避免重复”造轮子“，节约开发时间，对于该领域的开源项目的梳理，是保证开源软件供应链安全的基础；了解某一项目、组织的开源状况；了解某一领域的优秀开源项目目录，可以指示该领域的学习门径。

## 结语

开源项目目录是目录学在开源领域的落脚点。目前，开源项目的综合目录有较大的质量提升空间；专门目录较多但质量良莠不齐。

> **参考资料：**
> - 来新夏.古典目录学浅说[M].北京：北京出版社，2016.1
> - 余嘉锡.目录学发微；外一种：古书通例[M].长沙：岳麓书社，2009.12

[1]: https://www.oschina.net/project "OSCHINA 的开源软件库"
[2]: https://www.oschina.net/p/github "OSCHINA 的开源软件库收录的 GitHub 页面"
[3]: https://www.oschina.net/project/awesome?columnId=42 "这些游戏模拟器让你重温经典老游戏"
[4]: https://gitee.com/explore "Gitee 的开源软件探索页"
[5]: https://hellogithub.com/ "HelloGitHub"
[6]: https://gitee.com/openeuler/community/tree/master/sig/A-Tune "openEuler 社区的 A-Tune Sig 页"
[7]: https://kaiyuanshe.feishu.cn/wiki/UPrXwO0XailyQVkv4lGcED8inBe "开源社的开放黑客松项目介绍页"
[8]: https://gitee.com/openeuler/community "openEuler 社区的 openEuler/community 仓库"
[9]: https://github.com/vinta/awesome-python "awesome-python"

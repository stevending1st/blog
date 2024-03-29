---
title: 从物流与供应链看“软件供应链”
sticky: 0
copyright: true
date: 2022-10-31 23:57:48
categories:
tags:
- 物流
- 供应链
- 软件供应链
- 开源软件供应链
---

> 此文代表我粗浅的认知和思考，希望从一个“旧”视角，带给大家些许“新”思考。有很多不太严谨或正确的地方，亦希望各位师友批评指正。

“我在留学的时候，坐大巴遇见一个小伙子，我问他：‘你学什么专业的’？他说，供应链”，教授在课堂上平静地讲述了这样一个故事，这是我第一次听说“供应链”。

<!-- more -->

后来，随着手机产量被大家关注，手机厂商把“供应链”这样一个原本隐藏在系统之内，不容易被消费者察觉的东西暴露出来，这个概念也“飞入寻常百姓家”。伴随“供应链”概念普及的，还有人们对它的误解。一般人们对“供应链”的认知只停留在“物流”的层面上，往往忽视“资金流”和“信息流”。一般认为，“供应链”是围绕核心企业，通过对信息流、物流、资金流的控制，将供应商、制造商、仓库、配送中心、渠道商及用户有效组织起来，形成一个集计划、采购、制造、配送、退货等内容的网链结构模式。

在文章开始的那个故事，也存在一个“故事的供应链”——信息（故事）流向大体可以简化为我的老师到我和我的同学，我到看到文章的各位……随着 npm、pip 等包管理工具以及其可开源共享的包管理方式的流行，让人们切实认识到存在“软件的供应链”。

关于“软件供应链”的定义有许多不同看法，窃以为，根据“供应链”的基本概念，“软件供应链”应该是“全流程”的。悬镜安全与中国信通院联合制作的《软件供应链安全白皮书（2021）》认为“软件供应链”是“通过设计和开发阶段，将生产完成的软件产品通过软件交付渠道从软件供应链运输给最终用户”。《开源软件供应链安全研究综述》一文的作者认为：“开源软件供应链”是开源软件在开发和运行过程中, 涉及到的所有开源软件的上游社区、源码包、二进制包、第三方组件分发市场、应用软件分发市场, 以及开发者和维护者、社区、基金会等, 按照依赖、组合等形成的供应关系网络。窃以为，“软件供应链”是软件所有依赖（上游）包（软件）和下游产品设计、研发、运营、传播，软件产品设计、研发、运营，软件传播和使用的全流程网络。

“供应链”和“软件供应链”的主体有大的差异。“供应链”的主体往往是有形物质，其生产和运输过程往往受到时空和其装卸搬运工具的限制；“软件供应链”的主体是计算机软件，其生产和传播过程受到的空间限制比“供应链”弱很多。萧伯纳说过：“你有一个苹果，我有一个苹果，我们彼此交换，每人还是一个苹果；你有一种思想，我有一种思想，我们彼此交换，每人可拥有两种思想。”“供应链”的主体是客观的有形物质不随运输而复制生产；“软件供应链”的主体可以伴随传播而复制。一般情况下，使用“软件供应链”的上游产品的边际成本（单位产品的使用成本）要比使用“供应链”的上游产品的边际成本低得多。这些差异导致管理上有些区别。

需要指出的是，“供应链管理”侧重管理与产品相关的运营实体，而“软件供应链管理”侧重对产品可能出现的风险进行防控和应对。“供应链”中的上下游企业，往往知悉其上下游企业的生产情况；而在“软件供应链”中的开发者可能并不完全清楚自己的软件被哪些下游软件使用，这种情况在开源软件开发者中更为突出。在这种背景下，作为软件研发者，只能主动管理自己软件中依赖软件所产生的风险，理想情况下也应该积极主动修复自身风险，并公开通知下游软件及时更新版本（“软件供应链管理”无法像“供应链管理”中的产品强制召回，对于下游风险的控制，只能依赖下游软件维护者自己升级版本或更换技术方案来修复风险）。因此，“软件供应链管理”在某种程度上说就是“软件风险管理”。

和“供应链”的风险一样，“软件供应链”的风险也具有必然性、客观性、偶然性、不确定性、多样性、复杂性、传递性和放大性。一个上游软件的风险可能给一个已经平稳运行几年、十几年的系统带来不确定影响，有些影响如许可证更换甚至不会影响软件的正常运行，需要软件维护者积极关注上游软件动态。关于“软件供应链”风险分类，庄表伟老师的演讲《分类理解“开源供应链风险”》中已经有比较完整的思考可以参考，这里不再赘述。

对于“软件供应链”的风险管理，和“供应链”的风险管理一样，在风险发生前预防风险，评估风险带来的损失，参考二八定律，制定风险防范方案；在风险发生后积极应对，降低风险带来的损失。除此之外，在管理“软件供应链”时，还应积极构建风险监听系统，主动监听上下游软件风险，以避免损失。

我的老师在给我们讲述那段邂逅的同时，也想起了她当年在课间随意躺在小山包上晒太阳的美好时光，希望所有的软件都能在阳光下免受侵害，软件维护者能享受业余的每一份暖阳。

> **参考资料**
> - [供应链管理 - MBA智库百科 (mbalib.com)](https://wiki.mbalib.com/wiki/%E4%BE%9B%E5%BA%94%E9%93%BE%E7%AE%A1%E7%90%86)
> - [开源软件供应链安全研究综述 (jos.org.cn)](http://www.jos.org.cn/jos/article/abstract/6717)
> - 悬镜安全,中国信通院.软件供应链安全白皮书（2021）[R]
> - [分类理解“开源供应链风险”](https://www.bilibili.com/video/BV1xd4y1i7Wb)

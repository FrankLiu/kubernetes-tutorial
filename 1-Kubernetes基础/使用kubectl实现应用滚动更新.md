# 使用kubectl实现应用滚动更新

### 更新应用

用户需求：需要应用始终正常运行，开发人员每天需要部署新的版本_（一个简单例子，大家在玩游戏时常常碰到这类公告：8月8日凌晨：2点-6点服务升级，暂停所有服务.....）_。在Kubernetes中可以通过**滚动更新**（**Rolling updates** ）来完成。滚动更新通过Deployments实现应用实例在不中断、不停机情况下更新，新的Pod会逐步调度到可用的资源Node节点上。

在[前面的模块](http://docs.kubernetes.org.cn/122.html)中，我们对应用进行了[伸缩](http://docs.kubernetes.org.cn/122.html)，以运行多个实例。这是在不影响应用可用性的情况下执行更新的需求。更新时的Pod数量可以是数字或百分数\(pod\)来表示。在Kubernetes更新中，支持升级 / 回滚（恢复）更新。

## 滚动更新概述

（1）

![](https://d33wubrfki0l68.cloudfront.net/30f75140a581110443397192d70a4cdb37df7bfc/fa906/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates1.svg)

（2）

![](https://d33wubrfki0l68.cloudfront.net/678bcc3281bfcc588e87c73ffdc73c7a8380aca9/703a2/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates2.svg)

（3）

![](https://d33wubrfki0l68.cloudfront.net/9b57c000ea41aca21842da9e1d596cf22f1b9561/91786/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates3.svg)

（4）

![](https://d33wubrfki0l68.cloudfront.net/6d8bc1ebb4dc67051242bc828d3ae849dbeedb93/fbfa8/docs/tutorials/kubernetes-basics/public/images/module_06_rollingupdates4.svg)

与应用伸缩相似，滚动更新是实现流量负载均衡方式。

滚动更新允许以下操作：

* 将应用从一个环境升级到另一个环境（通过容器镜像更新）
* 回滚到之前的版本
* 持续集成和持续交付应用的零停机

在下面的[交互式教程](https://kubernetes.io/docs/tutorials/kubernetes-basics/update-interactive/)中，我们的应用将更新到一个新的版本，并执行回滚。




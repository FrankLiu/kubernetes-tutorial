# 使用kubectl实现应用伸缩

### 伸缩应用

在之前模块中，我们创建了一个[Deployment](http://docs.kubernetes.org.cn/317.html)，然后通过[Service](https://kubernetes.io/docs/concepts/services-networking/service/)暴露，Deployment创建的Pod来运行应用，当流量增加时，我们需要扩展应用来满足用户需求。

通过Deployment更改副本数可以实现**伸缩**。

## 伸缩概述

![](https://d33wubrfki0l68.cloudfront.net/043eb67914e9474e30a303553d5a4c6c7301f378/0d8f6/docs/tutorials/kubernetes-basics/public/images/module_05_scaling1.svg)

![](https://d33wubrfki0l68.cloudfront.net/30f75140a581110443397192d70a4cdb37df7bfc/b5f56/docs/tutorials/kubernetes-basics/public/images/module_05_scaling2.svg)

使用Deployment扩展能确保在新的可用Node资源上创建Pods，缩小比例将减少Pod的数量到理想状态。如果伸缩需求是0，将会终止Deployment指定的所有Pod。Kubernetes还支持[自动缩放](http://kubernetes.io/docs/user-guide/horizontal-pod-autoscaling/) Pods，本节将不做介绍。

运行应用将要考虑一些情况，需要将流量分配给所有实例。Service集成了负载均衡器，可以将网络流量分配到Deployment暴露的所有Pod中。Service将使用Endpoints持续监控运行的Pod，以确保仅将流量分配到可用的Pod。

下节将讨论如何在不停机的情况下进行滚动更新。现在让我们进入[在线终端进行伸缩我们的应用](https://kubernetes.io/docs/tutorials/kubernetes-basics/scale-interactive/)。




# Kubernetes 中查看Pods和Nodes

* [1Kubernetes Pod](http://docs.kubernetes.org.cn/115.html#Kubernetes_Pod)
* [2Pod概述](http://docs.kubernetes.org.cn/115.html#Pod)
* [3Node](http://docs.kubernetes.org.cn/115.html#Node)
* [4Node概述](http://docs.kubernetes.org.cn/115.html#Node-2)
* [5Troubleshooting with kubectl](http://docs.kubernetes.org.cn/115.html#Troubleshooting_with_kubectl)

## Kubernetes Pod

在模块[2中](http://docs.kubernetes.org.cn/113.html)创建Deployment时，Kubernetes会创建了一个[**Pod**](http://docs.kubernetes.org.cn/312.html)来托管应用。Pod是Kubernetes中一个抽象化概念，由一个或多个容器组合在一起得共享资源。这些资源包括：

* 共享存储，如 Volumes 卷
* 网络，唯一的集群IP地址
* 每个容器运行的信息，例如:容器镜像版本

_Pod模型是特定应用程序的“逻辑主机”，并且包含紧密耦合的不同应用容器。_

_Pod中的容器共享IP地址和端口。_

Pod是Kubernetes中的最小单位，当在Kubernetes上创建Deployment时，该Deployment将会创建具有容器的Pods（而不会直接创建容器），每个Pod将被绑定调度到Node节点上，并一直保持在那里直到被终止（根据配置策略）或删除。在节点出现故障的情况下，群集中的其他可用节点上将会调度之前相同的Pod。

## Pod概述

![](https://d33wubrfki0l68.cloudfront.net/fe03f68d8ede9815184852ca2a4fd30325e5d15a/98064/docs/tutorials/kubernetes-basics/public/images/module_03_pods.svg)![](/assets/module_03_pods.svg)![](/assets/import.png)

## Node

一个Pod总是在一个[（**Node）节点**](http://docs.kubernetes.org.cn/304.html)上运行，Node是Kubernetes中的工作节点，可以是虚拟机或物理机。每个Node由 Master管理，Node上可以有多个pod，Kubernetes Master会自动处理群集中Node的pod调度，同时Master的自动调度会考虑每个Node上的可用资源。

每个Kubernetes Node上至少运行着：

* Kubelet，管理Kubernetes Master和Node之间的通信; 管理机器上运行的Pods和containers容器。
* container runtime（如Docker，rkt）。

## Node概述

![](https://d33wubrfki0l68.cloudfront.net/5cb72d407cbe2755e581b6de757e0d81760d5b86/a9df9/docs/tutorials/kubernetes-basics/public/images/module_03_nodes.svg)

## Troubleshooting with kubectl

在第[2单元中](http://docs.kubernetes.org.cn/113.html)，使用了Kubectl 命令管理工具。我们继续在模块3中使用它来获取有关Deployment的应用及其环境信息。常见的操作可以通过以下kubectl命令完成：

* **kubectl get -**
  列出资源
* **kubectl describe**
  * 显示资源的详细信息
* **kubectl logs**
  * 打印pod中的容器日志
* **kubectl exec**
  * pod中容器内部执行命令

可以使用这些命令来查看应用程序何时部署、它们当前的状态是什么、它们在哪里运行以及它们的配置是什么。

现在我们已经了解了更多关于集群组件和命令的信息，[接下来让我们来探究一下应用](https://kubernetes.io/docs/tutorials/kubernetes-basics/explore-interactive/)。


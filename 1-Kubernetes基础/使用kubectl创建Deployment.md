# 使用 kubectl 创建Deployment

* [1目标](http://docs.kubernetes.org.cn/113.html#i)
* [2Kubernetes Deployments](http://docs.kubernetes.org.cn/113.html#KubernetesDeployments)
* [3在Kubernetes上部署第一个应用程序](http://docs.kubernetes.org.cn/113.html#Kubernetes)

### 目标

* 了解 Deployments 请求。
* 使用kubectl在Kubernetes上部署应用。

### Kubernetes Deployments

为了实现在Kubernetes集群上部署容器化应用程序。需要创建一个Kubernetes  [**Deployment**](http://docs.kubernetes.org.cn/317.html)**，**Deployment负责创建和更新应用。创建Deployment后，Kubernetes master 会将Deployment创建好的应用实例调度到集群中的各个节点。

应用实例创建完成后，Kubernetes Deployment Controller会持续监视这些实例。如果管理实例的节点被关闭或删除，那么 Deployment Controller将会替换它们，实现自我修复能力。

“在旧的世界中” ，一般通常安装脚本来启动应用，但是便不会在机器故障后自动恢复。通过在[Node节点](http://docs.kubernetes.org.cn/304.html)上运行创建好的应用实例，使 Kubernetes Deployment 对应用管理提供了截然不同的方法。

### 在Kubernetes上部署第一个应用程序

![](https://d33wubrfki0l68.cloudfront.net/3854a4db66ad3dd4ede078865eff41510eeba7c0/33ac5/docs/tutorials/kubernetes-basics/public/images/module_02_first_app.svg)

使用Kubernetes[Kubectl](http://docs.kubernetes.org.cn/61.html)（命令管理工具）创建和管理Deployment。Kubectl使用Kubernetes API与集群进行交互。在本学习模块中，学会在Kubernetes集群上运行应用所需Deployment的Kubectl常见命令。

创建Deployment时，需要为应用程序指定容器镜像以及要运行的副本数，后续可以通过Deployment更新来更改该这些信息; bootcamp的第[5](https://kubernetes.io/docs/tutorials/kubernetes-basics/scale-intro/)和第[6](https://kubernetes.io/docs/tutorials/kubernetes-basics/update-intro/)部分讨论了如何扩展和更新Deployment。

知道Deployment是什么，[来看看在线教程并部署你的第一个应用](https://kubernetes.io/docs/tutorials/kubernetes-basics/deploy-intro/)！




# Kubernetes 使用Service暴露应用

### Kubernetes Services概述

（凡人皆有一死来描述[pod](http://docs.kubernetes.org.cn/312.html)，没有比这跟准确的了）。事实上，Pod是有生命周期的。当一个工作节点\(Node\)销毁时，节点上运行的Pod也会销毁，然后通过ReplicationController动态创建新的Pods来保持应用的运行。作为另一个例子，考虑一个图片处理 backend，它运行了3个副本，这些副本是可互换的 —— 前端不需要关心它们调用了哪个 backend 副本。也就是说，Kubernetes集群中的每个Pod都有一个独立的IP地址，甚至是同一个节点上的Pod，因此需要有一种方式来自动协调各个Pod之间的变化，以便应用能够持续运行。

Enter Services。Kubernetes中的Service 是一个抽象的概念，它定义了Pod的逻辑分组和一种可以访问它们的策略，这组Pod能被Service访问，使用YAML [（优先）](https://kubernetes.io/docs/concepts/configuration/overview/#general-config-tips)或JSON 来定义Service，Service所针对的一组Pod通常由LabelSelector实现（参见下文，为什么可能需要没有 selector 的 Service）。

可以通过type在ServiceSpec中指定一个需要的类型的 Service，Service的四种type:

* ClusterIP
  （默认） - 在集群中内部IP上暴露服务。此类型使Service只能从群集中访问。
* NodePort
   - 通过每个 Node 上的 IP 和静态端口（NodePort）暴露服务。NodePort 服务会路由到 ClusterIP 服务，这个 ClusterIP 服务会自动创建。通过请求 
  &lt;
  NodeIP
  &gt;
  :
  &lt;
  NodePort
  &gt;
  ，可以从集群的外部访问一个 NodePort 服务。
* LoadBalancer
   - 使用云提供商的负载均衡器（如果支持），可以向外部暴露服务。外部的负载均衡器可以路由到 NodePort 服务和 ClusterIP 服务。
* ExternalName
   - 通过返回 
  `CNAME`
   和它的值，可以将服务映射到 
  `externalName`
   字段的内容，没有任何类型代理被创建。这种类型需要v1.7版本或更高版本
  `kube-dnsc`
  才支持。

更多不同类型Service的信息，请参考“[Using Source IP](https://kubernetes.io/docs/tutorials/services/source-ip/)[”](https://kubernetes.io/docs/tutorials/services/source-ip/)教程，[Connecting Applications with Services](https://kubernetes.io/docs/concepts/services-networking/connect-applications-service)。

使用ExternalName类型可以实现一种情况，在创建Service涉及未定义`selector`的示例，创建的Service `selector`不创建相应的Endpoints对象，可以通过手动将Service映射到特定Endpoints。

Kubernetes Service 是一个抽象层，它定义了一组逻辑的Pods，借助Service，应用可以方便的实现服务发现与负载均衡。

### Services和Labels

![](https://d33wubrfki0l68.cloudfront.net/cc38b0f3c0fd94e66495e3a4198f2096cdecd3d5/ace10/docs/tutorials/kubernetes-basics/public/images/module_04_services.svg)

如上图，A中Service 路由一组Pods的流量。Service允许pod在Kubernetes中被销毁并复制pod而不影响应用。相关Pod之间的发现和路由（如应用中的前端和后端组件）由Kubernetes Services处理。

Service 使用[label selectors](http://docs.kubernetes.org.cn/247.html)来匹配一组Pod，允许对Kubernetes中的对象进行逻辑运算，Label以key/value 键/值对附加到对象上。以多种方式使用：

* 指定用于开发，测试和生产的对象
* 嵌入版本Label
* 使用Label分类对象

你可以在使用  
`--expose`kubectl 创建 Deployment 的同时创建 Service 。



![](https://d33wubrfki0l68.cloudfront.net/b964c59cdc1979dd4e1904c25f43745564ef6bee/f3351/docs/tutorials/kubernetes-basics/public/images/module_04_labels.svg)



Label可以在创建时或以后附加到对象上，可以随时修改。

下一步：[使用在线互动教程](https://kubernetes.io/docs/tutorials/kubernetes-basics/expose-interactive/)




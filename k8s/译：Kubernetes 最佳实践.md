本文翻译自 [Jack Roper](https://jackwesleyroper.medium.com/) 的文章 [Kubernetes Best Practice](https://itnext.io/kubernetes-best-practices-d2bfb6fe3c19)。

> 译者：文章中作者从应用程序开发、治理和集群配置三个方面给出了一些 Kubernetes 的最佳实践，同时翻译过程中也加入了我过往的一些使用经验。有误的地方，也欢迎大家指正。

___

在这篇文章中，我将介绍一些使用 Kubernetes (K8s) 时的最佳实践。

作为最流行的容器编排系统，K8s 是现代云工程师掌握的事实标准。众所周知，不管使用还是维护 K8s 复杂的系统，因此很好地掌握它应该做什么和不应该做什么，并知道什么是可能的，将是一个好的开局。

这些建议包含 3 大类中的常见问题，即应用程序开发、治理和集群配置。

## 最佳实践目录

1.  使用命名空间
2.  使用就绪和存活探针（_译者注：还有启动探针_）
3.  使用自动缩放
4.  使用资源请求和约束
5.  使用 Deployment、DaemonSet、ReplicaSet 或者 StatefulSet 跨节点部署 Pod
6.  使用多节点
7.  使用基于角色的访问控制（RBAC）
8.  在外部托管Kubernetes集群（使用云服务）
9.  升级Kubernetes版本
10.  监控集群资源和审计策略日志
11.  使用版本控制系统
12.  使用基于Git的工作流程（GitOps）
13.  缩小容器的大小
14.  用标签整理对象（_译者注：或理解为资源_）
15.  使用网络策略
16.  使用防火墙

## 使用命名空间

K8s 中的命名空间对于组织对象、在集群中创建逻辑分区以及安全方面的考虑至关重要。 默认情况下，K8s 集群中有 3 个命名空间，`default`、`kube-public` 和 `kube-system`。

RBAC 可用于控制对特定命名空间的访问，以限制组的访问以控制可能发生的任何错误的爆炸半径，例如，一组开发人员可能只能访问名为 `dev` 的命名空间，并且无法访问 `production` 命名空间。 将不同团队限制在不同命名空间的能力对于避免重复工作或资源冲突可能很有价值。

还可以针对命名空间配置 `LimitRange` 对象，以定义部署在命名空间中的容器的标准大小。`ResourceQuotas` 还可用于限制命名空间内所有容器的总资源消耗。可以对命名空间使用网络策略来限制 pod 之间的流量。

## 使用就绪和存活探针

Readiness（就绪）和 Liveness（存活）探针本质上都是健康检查的类型。这些是在 K8s 中使用的另一个非常重要的概念。

就绪探针确保仅当 pod 准备好为请求提供服务时，才会将对 pod 的请求定向到它。如果它还没有准备好，那么请求将被定向到其他地方。为每个容器定义就绪探针很重要，因为在 K8s 中没有为这些设置默认值。例如，如果一个 pod 需要 20 秒才能启动并且缺少就绪探测，那么在启动期间定向到该 pod 的任何流量都会导致失败。就绪探针应该是独立的，并且不考虑对其他服务的任何依赖，例如后端数据库或缓存服务。

存活探针试应用程序是否正在运行以将其标记为健康。例如，可以测试 Web 应用程序的特定路径以确保其响应。如果不是，该 pod 将不会被标记为健康，并且探测失败将导致 `kubelet` 启动一个新的 pod，然后将再次对其进行测试。这种类型的探测用作恢复机制，以防进程无响应。

_译者：在 Kubernetes 1.18 引入了 StartUp（启动）探针。当容器启动时间较长（要花较长的时间完成初始化工作），此时应该使用启动探针。如果启动探针探测不成功，其他探针则不会生效。_

_译者：还有一点尽量为 Pod 内的所有容器都定义探针。_

## 使用自动缩放

在适当的情况下，可以使用自动缩放来动态调整 pod 的数量（Pod 水平自动缩放器，HPA）、pod 消耗的资源量（Pod 垂直自动缩放器, VPA）或集群中的节点数量（集群自动缩放器，CA），具体取决于 对资源的需求。

Pod 水平自动扩缩器还可以根据 CPU 需求扩展复制控制器、副本集或有状态集。

使用缩放也带来了一些挑战，例如不在容器的本地文件系统中存储持久数据，因为这会阻止水平自动缩放。相反，可以使用 PersistentVolume。

当集群上存在高度可变的工作负载并且可能根据需求在不同时间需要不同数量的资源时，集群自动缩放器非常有用。 自动删除未使用的节点也是省钱的好方法！

_译者：更多自动缩放的内容，可以浏览我之前翻译的[Kubernetes 的自动伸缩你用对了吗？](https://atbug.com/auto-scaling-best-practice-in-kubernetes/)；HPA 除了可以基于 CPU 指标伸缩，还可以基于内存，或者自定义指标，可以浏览[Kubernetes HPA 基于 Prometheus 自定义指标的可控弹性伸缩](https://atbug.com/kubernetes-pod-autoscale-on-prometheus-metrics/)_。

## 使用资源请求和约束

应设置资源请求和约束（可在容器中使用的最小和最大资源量）以避免容器在未分配所需资源的情况下启动，或集群用尽可用资源。

在没有限制的情况下，Pod 可以使用比所需更多的资源，从而导致可用资源总量减少，这可能会导致集群上的其他应用程序出现问题。节点可能会崩溃，并且调度程序可能无法正确调度新的 pod。

如果没有请求，无法为应用程序分配足够的资源，它可能会在尝试启动或执行异常时失败。

资源请求和限制以毫核和兆字节为单位定义可用的 CPU 和内存。请注意，如果进程超出内存限制，则该进程将终止，因此在所有情况下都可能不适合设置此值。如果容器超过 CPU 限制，则进程会受到限制。

## 使用 Deployment、DaemonSet、ReplicaSet 或者 StatefulSet 跨节点部署 Pod

永远不应该直接使用 Pod 运行。相反，为了提高容错性，Pod 应该始终作为 Deployment、DaemonSet、ReplicaSet 或 StatefulSet 的一部分。然后可以在部署中使用反亲和性规则跨节点部署 pod，以避免所有 pod 调度到同一个节点上运行，如果该节点发生故障可能会导致服务停止。

## 使用多节点

如果想提升容错性，在单个节点上运行 K8s 并不是一个好主意。集群中应该使用多个节点，以便可以在它们之间分散工作负载。

## 使用基于角色的访问控制（RBAC）

在 K8s 集群中使用 RBAC 对于正确保护系统至关重要。可以为用户、组和 service account 分配权限，以在特定命名空间（角色）或整个集群（ClusterRole）上执行允许的操作。每个角色可以有多个权限。要将定义的角色绑定到用户、组或 service account，使用 RoleBinding 或 ClusterRoleBinding 对象。

RBAC 角色授予应设置为使用最小权限原则，即仅授予所需的权限。例如，管理员组可能有权访问所有资源，而运维人员组可能能够部署，但不能读取 secret。

## 在外部托管Kubernetes集群（使用云服务）

在自己的硬件上托管 K8s 集群可能是一项复杂的工作。云服务将 K8s 集群作为平台即服务 (PaaS) 提供，例如 Azure 上的 AKS（Azure Kubernetes 服务）或 Amazon Web Services 上的 EKS（亚马逊弹性 Kubernetes 服务）。利用这一点意味着底层基础设施将由云服务商管理，并且可以更轻松地完成有关扩展集群的任务，例如添加和删除节点，而让工程师管理 K8s 集群上运行的内容本身。

## 升级Kubernetes版本

除了引入新功能外，新的 K8s 版本还包括漏洞和安全修复，这使得在集群上运行最新版本的 K8s 非常重要。对旧版本的支持可能不如新版本好。

然而，迁移到新版本时应谨慎对待，因为某些功能可能会被废弃，也可能会添加新功能。此外，在升级之前，应检查集群上运行的应用程序是否与较新的目标版本兼容。

## 监控集群资源和审计策略日志

监控 K8s 控制平面中的组件对于控制资源消耗非常重要。控制平面是 K8s 的核心，这些组件保持系统运行，因此对于正确 K8s 操作至关重要。 Kubernetes API、kubelet、etcd、controller-manager、kube-proxy 和 kube-dns 组成了控制平面。

控制平面组件可以以最常见的 K8s 监控工具 Prometheus 兼容的格式输出指标。

应该使用自动监控工具而不是手动管理告警。

可以在启动 kube-apiserver 时打开 K8s 中的审计日志记录，以便使用选择的工具进行更深入的调查。audit.log 将详细记录向 K8s API 发出的所有请求，并应定期检查集群上可能存在的任何问题。Kubernetes 集群默认策略在 audit-policy.yaml 文件中定义，可以根据需要进行修改。

Azure Monitor 等日志聚合工具可用于将日志从 AKS 发送到日志分析工作区，以便将来使用 Kusto 查询进行审讯。在 AWS Cloudwatch 上可以使用。第三方工具还提供更深入的监控功能，例如 Dynatrace 和 Datadog。

最后，应该为日志设置一个保留期，通常为 30-45 天左右。

## 使用版本控制系统

K8s 配置文件应该在版本控制系统 (VCS) 中进行管理。这带来了很多好处，包括提高安全性、启用更改的审计跟踪，并将提高集群的稳定性。应为所做的任何更改设置审批，以便团队可以在将更改提交到主分支之前对其进行评审。

## 使用基于Git的工作流程（GitOps）

K8s 的成功部署需要考虑团队使用的工作流程。使用基于 git 的工作流可以通过使用 CI/CD（持续集成 / 持续交付）管道实现自动化，这将提高应用程序部署效率和速度。CI/CD 还将提供部署的审计跟踪。Git 应该是所有自动化的单一事实来源，并将实现对 K8s 集群的统一管理。还可以考虑使用专用的基础架构交付平台，例如 Spacelift，它最近引入了 Kubernetes 支持。

## 缩小容器的大小

较小的映像大小将有助于加快构建和部署速度，并减少容器在 K8s 集群上消耗的资源量。应尽可能删除不必要的软件包，并应优先使用诸如 Alpine 之类的小型操作系统分发映像。较小的图像可以比较大的图像更快地拉取，并且消耗更少的存储空间。

遵循这种方法还将提供安全优势，因为恶意行为者的潜在攻击媒介将会减少。

## 用标签整理对象

K8s 标签是附加到对象用来组织集群资源的键值对。标签应该是有意义的元数据，提供一种机制来跟踪 K8s 系统中不同组件的交互方式。

K8s 官方文档中推荐的 Pod 标签包括名称、实例、版本、组件、部分和管理者。

标签也可以以类似于在云环境中对资源使用标签的方式使用，以跟踪与业务相关的事物，例如对象所有权和对象应属于的环境。

此外，还建议使用标签来详细说明安全要求，包括机密性和合规性。

## 使用网络策略

应该使用网络策略来限制 K8s 集群中对象之间的流量。默认情况下，所有容器都可以在网络中相互通信，如果恶意行为者获得对容器的访问权限，从而允许他们遍历集群中的对象，这会带来安全风险。网络策略可以在 IP 和端口级别控制流量，类似于云平台中的安全组的概念，以限制对资源的访问。通常，默认情况下应拒绝所有流量，然后应制定允许规则以允许所需流量。

## 使用防火墙

除了使用网络策略来限制 K8s 集群上的内部流量外，还应该在 K8s 集群前面放置防火墙，以限制来自外部环境对 API server 的请求。IP 地址应列入白名单并限制开放端口。

## 总结

在设计、运行和维护 Kubernetes 集群时遵循本文中列出的最佳实践将使你在现代应用程序之旅中走上成功之路！
# Tass Design



| Components      | Features                                                     | Data Structures                                              | Remarks |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------- |
| Serverless 中心 | 1. 负责业务流程的定义，负责函数的定义；<br>2. 知识共享；<br>3. Controller；<br>4. HTTP Triger。 | 1. Function / Workflow 数据结构；<br>2. 分支跳转的数据和知识利用率相关数据 |         |

## Technical selection

### Kubebuilder

目前打算使用 Kubebuilder 来构建 Controller，拟采用的版本是 [v2.3.1](https://github.com/kubernetes-sigs/kubebuilder/releases/tag/v2.3.1)，待讨论的一个点是版本选用，一周前（2021-02-18），Kubebuilder 推出了 [v3.0.0-beta.0](https://github.com/kubernetes-sigs/kubebuilder/releases/tag/v3.0.0-beta.0)，按照它以往的发布策略会在 1 个月后发布 v3.0.0-rc。这里我们是否需要考虑是 v3 beta 版。从它的发布信息来看，它的改变首先是版本依赖的一些变更（最关键是的 `controller-runtime-v0.5.0 -> controller-runtime-v0.7.0`），几个接口的调整，添加了对 Manager Deployment 的 liveness probe ，更多用户友好的提示等等（调整详情 🔎：[v3.0.0-alpha.0](https://github.com/kubernetes-sigs/kubebuilder/releases/tag/v3.0.0-alpha.0)，[v3.0.0-beta.0](https://github.com/kubernetes-sigs/kubebuilder/releases/tag/v3.0.0-beta.0)），从更新信息来看，v3 的总体更新篇幅没有那么大。

考虑到稳定性，采用 v2.3.1。

Kubebuilder 的简单使用：

1. 创建一个新的 crd：

   ```bash
   $ kubebuilder create api --group serverless --version v1alpha1 --kind Sample
   ```

   它会创建一个 `apiVersion` 为 `serverless.tass.io/v1alpha1` ，`kind` 为 `Sample` 的 crd；

2. 每次对 crd 定义文件（形如 `xxx_types.go`）的更新都需要 `make install`；

3. 启动 controller 的命令为 `make run`。

目前已收集到的可能对于开发 Kubebuilder 有帮助的教程：

* 官方 Cronjob Tutorial：[EN](https://book.kubebuilder.io/cronjob-tutorial/cronjob-tutorial.html) & [CH](https://cloudnative.to/kubebuilder/cronjob-tutorial/cronjob-tutorial.html)
  * 中文版和原文比有几处小出入，建议搭配原文；
  * 原文根据代码自动生成，可以直接参考官方 repo 示例中的代码（注意将分支调整为 v2）；
  * 已知该 Tutorial 安装 CRD 时会遇到的问题：[CronJob make install failed](https://github.com/kubernetes-sigs/kubebuilder/issues/1466)；
  
* [深入解析 Kubebuilder](https://juejin.cn/post/6844903952241131534)：介绍了 Kubebuilder 关键组件的作用；

* [使用 kubebuilder 创建 operator 示例](https://jimmysong.io/kubernetes-handbook/develop/kubebuilder-example.html)：极度精简版的 Tutorial；

* [熟悉又陌生的 k8s 字段：finalizers](https://developer.aliyun.com/article/772044)：Finalizers 的使用介绍；

* 其他一些在 Github 上的 Sample：[jetstack](https://github.com/jetstack)/**[kubebuilder-sample-controller](https://github.com/jetstack/kubebuilder-sample-controller)**，[ishankhare07](https://github.com/ishankhare07)/**[kubebuilder-controller](https://github.com/ishankhare07/kubebuilder-controller)** 和对应的[文章](https://dev.to/ishankhare07/writing-a-simple-kubernetes-controller-in-go-with-kubebuilder-ib8)；[tkestack](https://github.com/tkestack)/**[elastic-jupyter-operator](https://github.com/tkestack/elastic-jupyter-operator)**；

* [kubebuilder2.0学习笔记——进阶使用](https://segmentfault.com/a/1190000020359577)：包括 finalizer、控制器对 CRD 的 update status、kubebuilder 注释等。

## Architecture

### Workflow Definition

> 会在字段定义相对稳定后更新。

### Function Definition

> 会在字段定义相对稳定后更新。


# Tass Design



| Components      | Features                                                     | Data Structures                                              | Remarks |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------- |
| Serverless 中心 | 1. 负责业务流程的定义，负责函数的定义；<br>2. 知识共享；<br>3. Controller；<br>4. HTTP Triger。 | 1. Function / Workflow 数据结构；<br>2. 分支跳转的数据和知识利用率相关数据 |         |

## Technical selection

### Kubebuilder

目前打算使用 Kubebuilder 来构建 Controller，拟采用的版本是 [v2.3.1](https://github.com/kubernetes-sigs/kubebuilder/releases/tag/v2.3.1)，待讨论的一个点是版本选用，一周前（2021-02-18），Kubebuilder 推出了 [v3.0.0-beta.0](https://github.com/kubernetes-sigs/kubebuilder/releases/tag/v3.0.0-beta.0)，按照它以往的发布策略会在 1 个月后发布 v3.0.0-rc。这里我们是否需要考虑是 v3 beta 版。从它的发布信息来看，它的改变首先是版本依赖的一些变更（最关键是的 `controller-runtime-v0.5.0 -> controller-runtime-v0.7.0`），几个接口的调整，添加了对 Manager Deployment 的 liveness probe ，更多用户友好的提示等等（调整详情 🔎：[v3.0.0-alpha.0](https://github.com/kubernetes-sigs/kubebuilder/releases/tag/v3.0.0-alpha.0)，[v3.0.0-beta.0](https://github.com/kubernetes-sigs/kubebuilder/releases/tag/v3.0.0-beta.0)），从更新信息来看，v3 的总体更新篇幅没有那么大。

> 待讨论结果。

目前已收集到的可能对于开发 Kubebuilder 有帮助的教程：

* 官方 Cronjob Tutorial：[EN](https://book.kubebuilder.io/cronjob-tutorial/cronjob-tutorial.html) & [CH](https://cloudnative.to/kubebuilder/cronjob-tutorial/cronjob-tutorial.html)
  * 中文版和原文比有几处小出入，建议搭配原文；
  * 原文根据代码自动生成，可以直接参考官方 repo 示例中的代码（注意将分支调整为 v2）；
  * 已知安装 CRD 时会遇到的问题：[CronJob make install failed](https://github.com/kubernetes-sigs/kubebuilder/issues/1466)；
* [使用 kubebuilder 创建 operator 示例](https://jimmysong.io/kubernetes-handbook/develop/kubebuilder-example.html)：Jimmy Song 的，还没看过，不知道好坏；
* [深入解析 Kubebuilder](https://juejin.cn/post/6844903952241131534)：粗略扫过一眼，感觉不错，待阅读。

## Architecture

Todo




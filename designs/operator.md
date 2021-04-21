# Tass Design



| Components | Features                                                     | Data Structures                                              | Remarks |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------- |
| Operator   | 1. 负责业务流程的定义，负责函数的定义；<br>2. 知识共享；<br>3. Controller；<br>4. HTTP Triger。 | 1. Function / Workflow 数据结构；<br>2. 分支跳转的数据和知识利用率相关数据 |         |

## CRD Types

### Workflow Definition

> 会在字段定义相对稳定后更新。

### Function Definition

> 会在字段定义相对稳定后更新。

### WorkflowRUntime Definition

> 会在字段定义相对稳定后更新。

## Cli

Cli 主要负责以下功能：

* Function 的增删改查以及测试一个 Function 是否可正常运行；
* todo...

下图展示了创建一个 Function 涉及的主要流程：

<img src="img/create-fn.png" style="zoom:30%;" />

* 用户输入 `tass function create --name sample --ns default --env golang --code sample.go`；
* Cli 根据 code 参数指定的位置寻找对应代码文件，将文件存储至对应存储服务中；
* Cli 根据剩余参数将 Function Metadata 发送至集群的 Function Operator，由 Operator 负责后续对应 Function 的创建。

## Guide

### Kubebuilder

目前打算使用 Kubebuilder 来构建 Controller，拟采用的版本是 [v2.3.1](https://github.com/kubernetes-sigs/kubebuilder/releases/tag/v2.3.1)。本质上来说，Kubebuilder 是 Kubernetes Operator 的一套构建工具，通过使用 `kubebuilder` cli 来自动生成一些代码，

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
* [熟悉又陌生的 k8s 字段：finalizers](https://developer.aliyun.com/article/772044)：Finalizers 的使用介绍；
* [kubebuilder 2.0 学习笔记——进阶使用](https://segmentfault.com/a/1190000020359577)：包括 finalizer、Controller 对 CRD 的 update status、kubebuilder 注释等；
* 其他一些在 Github 上的 Sample：[jetstack](https://github.com/jetstack)/**[kubebuilder-sample-controller](https://github.com/jetstack/kubebuilder-sample-controller)**，[ishankhare07](https://github.com/ishankhare07)/**[kubebuilder-controller](https://github.com/ishankhare07/kubebuilder-controller)** 和对应的[文章](https://dev.to/ishankhare07/writing-a-simple-kubernetes-controller-in-go-with-kubebuilder-ib8)；[tkestack](https://github.com/tkestack)/**[elastic-jupyter-operator](https://github.com/tkestack/elastic-jupyter-operator)**。


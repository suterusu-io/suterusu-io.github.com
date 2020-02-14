---
title: "为什么要实现一个自己的客户端"
date: 2020-02-14T16:47:46+08:00
image_webp: images/blog/Suter-banner.webp
image: images/blog/Suter-banner.jpg
draft: false
---

# Suterusu项目为Substrate生态添砖加瓦
Substrate项目为区块链的构建和应用开发提供了一套灵活且完善的框架，也正是因为其灵活性, 使用substrate来开发应用或者区块链的项目和个人很容易使用自己熟悉的语言和框架来实现和自身业务相关的组件。 Suterusu项目在对零识证明的创新的基础之上构件一套支持不同区块链的隐私保护协议，需要根据自身的开发和实际需求，实现一套更合适的客户端。在此背景下，Suterursu项目使用OCaml函数式语言开发了suter-client .此客户端通过标准的RPC调用与基于substrate的区块链进行交互，项目本身以Apache-2协议授权。

Suter_chain的代码目前已经公布在github上，目前还处于开发阶段，功能和特性在不断的充实中。 [Suter_client](https://github.com/suterusu-team/suter_cli)


# 为什么要实现一个自己的客户端

* 零知识证明做为一项比较复杂的密码学技术，由于其复杂性很难被多数开发者和用户使用，并且零知识证明本身的实现也是百花齐放，我们项目的核心是改进的零知识证明，如何让更多的人能在项目和开发中使用专业的ZKP密码学库是我们想更好的推广零识证明的一个重要途径，在原生的substrate客户端来提供支持会有些局限性。
Suter的客户端的核心是实现了一套DSL(Doamin specific language), 翻译成中文叫做领域特定语言。 通过实现DSL，零识证明的使用会更加通用，容易和安全。 

* Suter_CLI DSL的特点
  * 易用性和灵活扩展性
启动一个ZKP交易有时需要通过多次和公链node的RPC交互，通过DSL可以定义好所有交易逻辑，然后触发DSL runtime executor批量执行。DSL就好比正则表达式，用户只需要关注指定业务规则逻辑，然后触发执行即可。如果没有正则表达式的话，一些简单的匹配操作需要实现各种不同的库来处理，且当需要新功能时又需要增加不同的库，扩展性大打折扣。实用性上远远不如正则表达式任意灵活组合，而Suter_CLI的DSL就好比ZKP领域的正则表达式。

  * 通用性
现在ZKP领域有不同的实现方案，接口各一，这对于用户/开发者来说是很大的挑战，如果想切换方案需要根据不同zkp方案的API library重新适配。Suter_CLI通过DSL打造一个ZKP领域的通用标准，用户只需要专注基于DSL实现ZKP业务逻辑，而无需关注底层具体ZKP方案的实现。通过这样解耦，用户方案的通用性可以大幅提升，可以轻松的在任何只要实现了DSL Runtime Executor的平台。还是拿正则表达式举例子，任何项目和语言都可以解析实现正则表达式的解析运行，用户/开发者只需要专注写好正则表达式就行。对应DSL，用户只需要专注用DSL写好ZKP业务逻辑。

  * 安全性和可调试
通用引入DSL解析层，可以更容易的对用户ZKP逻辑进行各类参数安全检查和逻辑验证，比如可以通过跟Suter_Chain的后端配合，对ZKP逻辑进行形式化验证，从而保证系统的安全性。

**关于DSL的语法语义以及更多内容，敬请期待我们后续系列文章** 

## Suter_client的架构和组成
Suter_client架构如图：
![Suter_client architecture](/images/blog/suter_cli.jpg)

Suter_CLI主要由三个核心组件构成
* 接口层
  * Suter_CLI会实现各种ZKP API的DSL Scripts Library，再封装出 JS API或者Ocaml API(其中sJS API由Ocaml自动生成）给普通用户使用
  * 专家用户：可以直接基于DSL开发，也可以直接调用我们封装的DSL Scripts Library

* DSL Runtime Executor
  * DSL的核心执行器, 定义和解析DSL语法
  * 安全检查审计和执行DSL命令

* Connection Component
  * 负责和底层公链Node的连接交互

# 如何安装和体验
  * 安装ocaml环境，确保ocaml的版本高于4.7.0版本
  * 下载代码并编译
```
git clone https://github.com/suterusu-team/suter_cli 
cd suter_cli
./configure.sh 
make 
```
* 启动substrate节点，并确保其监听9944端口
 
```
./wsclient.native -url http://127.0.0.1:9944
```

# Stuer_client提供了两种方式
* 交互式命令行

```
> wsclient.native -url http:127.0.0.1
```

如上启动交互式命令行后，你可以像这样输入和执行命令：

```
> id := [0]
//An extended json format which can reuse local variables in json fields.
> @send id |> chain_getBlockHash
```

以上命令会返回chain的第0个Block的Hash值:

```
> Response: "0x2895bf7b698e2efaa18eb3a1f0980f983a7778ca74a9abf123e1d08f9789c66b"
```

你也可以把返回值存储到本地变量供将来使用：

```
> hash := @send id |> chain_getBlockHash
```

这样，节点的chain_getBlockHash api就被调用成功了。

* 脚本方式

比如直接写好脚本
chain_getBlockHash.sbl

```
> id := [0]
> @send id |> chain_getBlockHash
```

```
> wsclient.native -url http:127.0.0.1  chain_getBlockHash.sbl
```






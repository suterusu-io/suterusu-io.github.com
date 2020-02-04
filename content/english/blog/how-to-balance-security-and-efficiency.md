---
title: "How to balance security and efficiency"
date: 2019-12-19T11:19:25+08:00
image_webp: images/blog/Suter-banner.webp
image: images/blog/Suter-banner.jpg
isCJKLanguage: true
---

近期 suterusu 公开的黄皮书提出了一个新的适用于智能合约平台的保密支付方案。目前本人能找到的同类型完整方案仅有由斯坦福大学和 Visa 研究部门共同合作的一篇文章 Zether。我们黄皮书的基本框架和 Zether 有一定相似之处，但 Zether 的方案在算法层面上基本上还是比较传统的椭圆曲线密码的那一套东西。事实上，正如黄皮书所述，Zether 的密码算法可看作基于传统椭圆曲线密码的保密支付方案的一个变体，其主要区别在于原保密支付中使用的承诺方案被替换成 Elgamal 加密方案，对应的零知识证明方案也做了修改。

Suter 黄皮书方案使用的保密支付密码算法是基于 Class groups of quadratic imaginary order 的，在算法设计上借鉴了近期这个领域的一些新技术进展。我们将这些新技术用于改进传统的基于 RSA 群的 range proof 方案。目前性能方面表现最好的基于 RSA 群的 range proof 方案是由法国名校巴黎高等师范学院和法国国家科学院等单位的三位密码学家提出的。但基于 RSA 群的方案存在一个问题就是需要 trusted setup。另外，原方案在证明者自由选择数字承诺使用的 group base 时是没法保证方案本身的安全性的，这也是为何我们需要重新设计一个 range proof 方案的原因之一。

我们和基于 RSA 群的 range proof 方案的原作者之一合作重新设计一个基于 class groups 的 range proof 方案。该方案的证明大小为常数，无需 trusted setup，且能保证证明者自由选择承诺使用的 group base 时方案的安全性。这样做的好处在于 range proof 方案能和我们设计的基于 class group 的 proof of consistent balance encryption 方案对接，从而能构造出一个完整的支持账户模型的保密支付方案。

我们接下来将进一步改进现方案效率，并将其与其他可选的基于椭圆曲线的密码方案做比较，以选择最优方案作为 Suter 跨链隐私方案的底层算法。此外，这篇黄皮书还介绍了 Suter 区块链后续使用的 POW 和 POS 混合共识协议。

Suterusu 项目设计实现的零知识证明技术的应用场景首当其冲的当然是各种支付模型下的隐私保护支付。除外，我们方案的设计思路也可以用于改进无需 trusted setup 的盲签名方案，这个可以作为基于隐私保护个人注意力 / 数据金钱化的网络经济的底层密码方案。事实上，盲签名方案是目前已有超过一千万用户，coinmarketcap 排名 30 左右的 brave 浏览器 / 基本注意力币项目的核心技术。目前 Suterusu 项目正积极寻求和这方面项目合作的可能性。此外，我们也正和几个排名 100 以内公链项目洽谈合作事宜。

随着各种隐私数据法规包括加州消费者隐私法规 (California consumer privacy act) 的推出，企业在使用个人数据时的透明性和合规性方面将会有实质性的加强。账户模型下的高效保密支付方案在促进细粒度的个人数据金钱化过程的自动化和透明化方面将起到至关重要的作用。而数据 / 注意力的金钱化是现有网络商业化的核心机制，这个应用场景的商业前景不可限量。

最后，黄皮书的保密支付方案也可用于设计隐私保护的链上管理机制。本人目前正在参与写作一篇探讨这方面技术应用的综述文章，敬请到时关注。

---
time: 2020-3-5



---

# Go 多模块构建方案

思考：为什么 Golang 没有像 `Maven` 或者 `Cargo` 的构建工具？

个人猜测是遵循了[奥卡姆剃刀](https://zh.wikipedia.org/wiki/%E5%A5%A5%E5%8D%A1%E5%A7%86%E5%89%83%E5%88%80) 的`Do not multiply entities beyond necessity`的设计哲学。

> “切勿浪费多余工夫去做本可以较少工夫完成之事”

> ​	在[自然科学](https://zh.wikipedia.org/wiki/自然科学)中，奥卡姆剃刀被作为[启发法](https://zh.wikipedia.org/wiki/启发法)技巧来使用，更多地作为帮助[科学家](https://zh.wikipedia.org/wiki/科学家)发展理论模型的工具，而不是在已经发表的理论之间充当裁判角色。[[7\]](https://zh.wikipedia.org/wiki/奥卡姆剃刀#cite_note-fn_(100)-7)[[8\]](https://zh.wikipedia.org/wiki/奥卡姆剃刀#cite_note-fn_(101)-8)在[科学方法](https://zh.wikipedia.org/wiki/科学方法)中，奥卡姆剃刀并没有被当做逻辑上不可辩驳的定理或者科学结论。在科学方法中对简单性的偏好，是基于[可证伪性](https://zh.wikipedia.org/wiki/可证伪性)的标准。对于某个现象的所有可接受的解释，都存在无数个可能的、更为复杂的变体：因为你可以把任何解释中的错误归结于[特例假设](https://zh.wikipedia.org/wiki/特例假設)，从而避免该错误的发生。所以，较简单的理论比复杂的理论更好，因为它们更加可检验。

这其实就是师父一直强调的:

> ”把复杂的事情简单化，而不是把简单的事情复杂化”

在我最近的工程实践中，我个人总结出了两种构建方案，而后者我认为是比较优质的，甚至我猜测这就是官方的思路。

- Makefile 构建

  这里主要参考了[dubbo-go-samples](https://github.com/apache/dubbo-go-samples) 提供的 [build/Makefile](https://github.com/apache/dubbo-go-samples/blob/master/build/Makefile) 的构建方案。

- 容器化构建

  使用 `docker-compose.yml` 进行容器化的构建，这个方案不仅可以构建单体应用，而且是可以作为单主机容器编排工具使用的。

这倒是给了我以下经验：

- 当做一个方案前，一定要思考为什么要做这个方案，为什么现有的方案没有很好的解决这个问题？避免造轮子走弯路。
- 而如果一个新方案牵扯到了许多的新的工具链，应该有足够的勇气去尝试实践，因为拿着旧地图永远找不到新大陆。

因为一旦你的方案做偏了，后面我们会需要花大量的时间在弥补旧方案带来的不足，而这些补丁会让整个方案犹如没有基础的楼阁，岌岌可危。而且越往后面，迭代成本可能会越来越高。我们做方案本身求的可持续和性价比。所以前期的不调研和思考，会带来后期的种种困难和成本。

但我还会有个疑惑，人在对方案下的工具都未知的情况下，且没有很好的实践时应该怎么做？

我现在的解决方案就是：

- 去科学上网 Google 资料，看最前沿的实践文章
- 开源项目直接提 Issue，和开发者面对面

自己现在的做事遵从以下原则：

- 避险
- 高收益
- 稳定的可持续
- 迭代周期足够短

虽然有些不可能三角的意味，但这不就是做方案的有趣之处 - 平衡，这都比盲目的去造轮子的收益。

待续，我要继续做项目的 `docker-compose.yml`实践了。

## 教训

这次教训惨痛，在时间 `docker` 的 `networks` 部分，由于没有从一开始看手册，导致摸索了很久才知道 `docker network ls` 这条指令。这里要感谢 [docker容器网络 - 同一个host下的容器间通信](https://zhuanlan.zhihu.com/p/137539975) 这篇文章引路。但也要抱怨一下，我找了很多文章才找到，甚至是官方文档，官网应该把 docker-compose 的方式作为主要的方式来进行文章的书写，而不是命令行的方式。

所以，今后一定在实践一个框架的时候，一定要把它的全貌了解的差不多，再去实践细节。


---
time: 2020-3-5




---

# 

# 单元测试

以 `Go` 语言为实践对象

## 参考

《软件测试的艺术》
《软件测试-第二版》

[coursera - 软件测试](https://www.coursera.org/learn/ruanjian-ceshi#syllabus)

## TODO

[什么是打桩？](https://www.zhihu.com/question/397159494/answer/1308788520)

## 测试模式

## 测试

[TDD]()

[BDD]()，Behavior-Driven Development，行为测试框架，目前主流的有：

- [Ginkgo](https://blog.gmem.cc/ginkgo-study-note)

  相关的实践有 [dbtest](https://github.com/dche423/dbtest.git)
-

## 原则

参考自 [你懂SOLID原则吗？](https://mp.weixin.qq.com/s/JOVSkcC48qwoaByxUtgcFA)

- 单一职责原则

一个方法只干一件事情。

- 开闭原则
- 里氏替换原则

子类要与父类的行为保持一致

- 接口隔离原则
- 依赖倒置原则

## 黑盒测试

黑盒测试如下
### 参考

[一个高效测试用例设计的解决方案！](https://testerhome.com/topics/17554)

这里可以参考公众号
-  [软件测试 BeTester](https://zhuanlan.zhihu.com/p/75073232)
-  [软件测试打怪升级](https://www.zhihu.com/column/c_1185258897522274304)



意味着不看代码就进行测试，主要的测试方法有：

### 等价类划分设计

就是把输入域的值分为若干的部分（选出一个代表来）

#### 分类

- 有效等价类

  合理的、有意义的

- 无效等价类

  没有意义的、不合理的

#### 等价划分方法

##### 按区域划分

比如学生成绩划分，有效值为[0，100]

##### 按数值（集）划分

输入数据是离散的数据集，比如购买地铁票，输入的数值有：1元，5元，10元，20元。

##### 按限制条件或规则划分

依赖产品规格要求或限制，使得我们只能在特定范围内进行输入。注册的时候输入手机号码，手机号码有相应的规则约束。否则非法

##### 等价类实例

- 微信红包

  有效等价类： 0 < x <= 200

  无效等价类：x<0 或者x>200

- 判断是否是一个一线城市

  有效等价类：北京、上海、广州、深圳

  无效等价类：北上广深除外

##### 注册邮箱，对用户名进行校验

有各种的约束

### 边界值设计

通过对临界条件的测试分析方法。考试成绩只差“半分”，回到家却是一种天上和炼狱的待遇。

#### 概述

##### 定义

就是对输入或输出的边界值进行测试，作为等价划分法的补充，其测试用例来自**等价类**的边界。

##### 等价类差异

- 边界值测试不是从某一个等价类中随便挑一个作为代表，而是要覆盖该等价类的所有边界的测试条件
- 边界值测试不仅考虑输入条件，还要考虑输出结果产生的测试情况。比如：在高速收费站，其收费结果只有“找零”或“无需找零”。当遇到没有现金的司机会怎么样？这就是从输出结果的边界考虑的。 

#### 划分方法

##### 数值型边界

- 上点：边界上的点，闭内开外（闭指闭区间；开指开区间）
- 离点：离上点最近的点称为离点，开内闭外
- 内点：区间内的任意一点

min-,min,min+,normal,max-,max,max+

##### 字符型边界

可以转换为数值型边界，测试成绩，可以转换为的区间[0，100]进行边界测试分析

一个字符串，第一个字符和最后一个字符为边界。比如邮箱只能数字或者字母开头

##### 空间型边界

物理空间或者位置，或者计算机的磁盘存储，所以就不是数值，而是一个结构体

##### 实例

- 微信红包金额限制
- 邮箱长度限制
- 机场电子围栏（无人机）

### 正交设计

多个因素的水平组合

#### 验证

- 正交验证
- 配对验证

#### 失效模式

- 单失效

由单个因素引起
- 双失效

由两个因素引起，针对所有的参数进行两两组合
- 多失效

有多个因素引起，通过两两组合进行测试，无法抱枕测试的充分性。

#### 概念
- 因素

在试验中，影响试验结果的变量
- 水平

因素所处的状态
- 因素数

在实验中，影响试验结果的变量个数
- 水平数

因素所包含的状态集合数量

####  特点
- 分布均匀

任一列中，任一因素的水平（状态）出现的次数相同
- 整齐可比

任两列中，任意一个水平组合出现的次数相同

### 状态迁移设计

[状态迁移测试](https://mp.weixin.qq.com/s?__biz=MzI2NDk1NTU4Ng==&mid=2247484675&idx=1&sn=2f4ec1165a40009785d6be7412cc2722&chksm=eaa5f6aeddd27fb89563be0589de400d0c0673f8abc45bddb96662bbff7c3af51d718cbfc761&token=866530587&lang=zh_CN#rd)

#### 有限状态机

有 3 个要素

- 现态

  当前所处的状态
  
- 条件

  事件，当一个条件被满足后，触发一个动作，或者执行一次状态迁移
  
- 次态

   条件满足后，要迁往的状态

#### 状态迁移

把系统的状态抽象出来，对抽象的状态相互之间的切换条件和路径进行标记，形成有限状态机。

>  注意事项
>
> 1. 不要把条件/事件和状态混为一谈
> 2. 避免出现状态的遗漏
> 3. 状态变化后可以回到原先状态

#### 状态迁移步骤

1. 根据被测对象的需求提取状态
2. 绘制状态迁移图
3. 确定测试强度，转换成状态树
4. 选择测试数据，设计测试用例

#### N Switch

根据资源的投入来选择 switch 的强度

### 判定表设计

[判定表](https://mp.weixin.qq.com/s?__biz=MzI2NDk1NTU4Ng==&mid=2247484646&idx=2&sn=32d78e42548285ad1aeb8ac4259538fd&chksm=eaa5f74bddd27e5d83e99501becfb19b20d3a110d79f8b1b2c33c39c343a00f8876d28cd528a&token=2135977015&lang=zh_CN#rd)

#### 1. 什么是？

也可以称之为：决策表，把复杂的逻辑关系和多种条件组合的情况表达得具体明确

#### 2. 组成元素

- 条件桩

  被测对象的所有输入

- 条件项

  被测对象的输入取值

- 动作桩

  被测对象可能采取的操作/表现

- 动作项

  在各个条件项的组合下，被测对象所采取的动作/表现

思想品质、身体、学习对应的条件状

成为三好学生和没成为三号学生便是动作桩

#### 3. 判定表的优缺点及适用范围

### 因果图

#### 什么是？

[因果图](https://mp.weixin.qq.com/s?__biz=MzI2NDk1NTU4Ng==&mid=2247484646&idx=1&sn=5bee9e8350cfee93b43187287fe0b0fa&chksm=eaa5f74bddd27e5ddd05040c29114d3b6d43015161fc477a07f8254e702bb9c6d957b0288910&token=2135977015&lang=zh_CN#rd)，是一种用于输入与输入，输入与输出存在依赖与约束关系的被测对象。因果图是一种利用图解法分析输入的各种组合情况。

等价类和边界值分析法也是对输入条件进行测试分析，只是输入条件之间不存在关系或者约束 ，且必须相互独立（等价类的原则之一）

#### 图的关系

##### 因果关系

1. 恒等

   1-1，0-0

   商场购物，买单才会有打印凭条，没有买单就不会打印

2. 非~

   1-0，0-1

   手机逛淘宝，有网络不提示网络异常，没有网络则提示网络异常

3. 或U

   手机平板、电脑、电视都可以看视频

4. 与^

   手机要有电、网络、信号才能上网。没有则不能上网

##### 条件约束

1. 异或/ 互斥

   至多一个为1

   赴约，只能选择步行、自行车、打车、坐地铁、开车中的一个，也可以都不选。

2. 或

   至少一个必须是1

   手机平板、电脑、电视都可以看视频，但必须选择至少一个

3. 唯一

   有且只有一个1

   坐地铁，必须从交通卡、微信支付、临时票选择其中一个

4. 要求

   出手投篮，必须拥有球权，如果没有出手投篮，无法确定是否拥有球权

5. 强制

如果在公司，必定不在家，但如果不在公司，未必在家。

#### 分析步骤

#### 实例



## Mock 使用

数据需要隔离，参考 [Golang 单元测试：有哪些误区和实践？](https://developer.aliyun.com/article/778487) 所以使用 `sqlmock` 来实现，比如 [sqlmock-blog-demo](https://github.com/DATA-DOG/go-sqlmock/tree/master/examples/blog)

适合使用 mock/stub 场景是

- 数据库连接
- 文件I/O

## 注意事项

- 尽量不对 `http` 和 `net`库使用 mock，这样可以覆盖较为真实的场景

## 实践参考

参考 [dubbo-go](https://github.com/apache/dubbo-go) 的单元测试写法

## 避雷专区

使用 `sqlmock` 时，遇到的 [事务导致异常的ISSUE](https://github.com/DATA-DOG/go-sqlmock/issues/210) 的问题

- 因为在调用过程中，会发生调用栈的问题

```
call to Query 'SQL' with args, was not expected, next expectation is: ExpectedBegin => expecting database transaction Begin
```


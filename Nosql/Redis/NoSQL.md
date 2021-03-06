# NoSQL：

Redis理解

> KV 键值对
>
> Cache 快取
>
> Persistence 编写

3V3高：

> 大数据时代3V ： 
>
> Volume 海量
>
> Variety 多样
>
> velocity 实时
>
> 互联网需求3高：
>
> 高并发
>
> 高可扩
>
> 高性能

CAP+BASE

[分布式数据库中的CAP原理(了解)](https://blog.csdn.net/a909301740/article/details/80149552)
CAP定理：

Consistency(一致性), 数据一致更新，所有数据变动都是同步的
Availability(可用性), 好的响应性能
Partition tolerance(分区容错性) 可靠性
P: 系统中任意信息的丢失或失败不会影响系统的继续运作。
定理：任何分布式系统只可同时满足二点，没法三者兼顾。

CAP理论的核心是：一个分布式系统不可能同时很好的满足一致性，可用性和分区容错性这三个需求，

因此，根据 CAP 原理将 NoSQL 数据库分成了满足 CA 原则、满足 CP 原则和满足 AP 原则三 大类：

CA - 单点集群，满足一致性，可用性的系统，通常在可扩展性上不太强大。
CP - 满足一致性，分区容忍性的系统，通常性能不是特别高。
AP - 满足可用性，分区容忍性的系统，通常可能对一致性要求低一些。
CAP理论就是说在分布式存储系统中，最多只能实现上面的两点。

而由于当前的网络硬件肯定会出现延迟丢包等问题，所以分区容忍性是我们必须需要实现的。

所以我们只能在一致性和可用性之间进行权衡，没有NoSQL系统能同时保证这三点。

> 说明：C：强一致性 A：高可用性 P：分布式容忍性

举例：

CA：传统Oracle数据库

AP：大多数网站架构的选择

CP：Redis、Mongodb

## ACID是什么？（传统数据库）

> A：Atomicity 原子性
>
> C: Consistency 一致性
>
> I： Isolation 独立性
>
> D： Durability 持久性

## CAP是什么？（Nosql）

> C： Consistency 强一致性
>
> A：Availability 可用性
>
> P：Partition tolerance 分区容错性

CAP三进二![CAP](D:\Boke\Databases\Nosql\Redis\CAP.jpg)

什么时候使用 强一致（C）什么时候使用 高可用（A）呢？

金融，电商，传统的是AP

为什么呢？（两者其害取其轻）

是选择高精确的浏览数、点赞数还是网站选择可用性呢？

### 关于数据库方面的个人想法：

C-A-P是个相对的概念，或许可以使用缓存的形式来减少处理的信息量？

处理过多，P为需一定， C与A成反比，一致性需求高（c），可用性低，以添加外部的缓存来增加a，减少过多的重复操作，从而提高可用性

# BASE：（≈  反ACID）

> 基本可用 （Basiclly Available）
>
> 软状态 （Soft State）
>
> 最终一致性 （EventUally consistent）

高峰时牺牲一致性，保证可用性。AP

但高峰过后需要最终结果一致性

> 思想： 通过让系统对某一时刻数据一致性的要求来换取系统整体伸缩性和性能上改观，

## 浅谈分布式概念：

分布式：不同的多台服务器上面部署**不同**的服务模块，他们之间通过RPC/RMI之间通信和调用，对外提供服务和组内协作

集群（人多力量大）：不同的多台服务器上部署**相同**的服务模块，通过分布式调度软件进行统一的调度，对外提供服务和访问


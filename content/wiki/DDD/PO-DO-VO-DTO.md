**VO（View Object）**：视图对象，用于展示层，它的作用是把某个指定页面（或组件）的所有数据封装起来。 用户提交的数据 req

**DTO（Data Transfer Object）**：数据传输对象，这个概念来源于J2EE的设计模式，原来的目的是为了EJB的分布式应用提供粗粒度的数据实体，以减少分布式调用的次数，从而提高分布式调用的性能和降低网络负载，但在这里，我泛指用于展示层与服务层之间的数据传输对象。将VO转换为服务(DO)所需要的参数.

**DO（Domain Object）**：领域对象，就是从现实世界中抽象出来的有形或无形的业务实体。

**PO（Persistent Object）**：持久化对象，它跟持久层（通常是关系型数据库）的数据结构形成一一对应的映射关系，如果持久层是关系型数据库，那么，数据表中的每个字段（或若干个）就对应PO的一个（或若干个）属性。


**VO与DTO的区别**

大家可能会有个疑问（在笔者参与的项目中，很多程序员也有相同的疑惑）：既然DTO是展示层与服务层之间传递数据的对象，为什么还需要一个VO呢？对！对于绝大部分的应用场景来说，DTO和VO的属性值基本是一致的，而且他们通常都是POJO，因此没必要多此一举，但不要忘记这是实现层面的思维，对于设计层面来说，概念上还是应该存在VO和DTO，因为两者有着本质的区别，DTO代表服务层需要接收的数据和返回的数据，而VO代表展示层需要显示的数据。
用一个例子来说明可能会比较容易理解：例如服务层有一个getUser的方法返回一个系统用户，其中有一个属性是gender(性别)，对于服务层来说，它只从语义上定义：1-男性，2-女性，0-未指定，而对于展示层来说，它可能需要用“帅哥”代表男性，用“美女”代表女性，用“秘密”代表未指定。说到这里，可能你还会反驳，在服务层直接就返回“帅哥美女”不就行了吗？对于大部分应用来说，这不是问题，但设想一下，如果需求允许客户可以定制风格，而不同风格对于“性别”的表现方式不一样，又或者这个服务同时供多个客户端使用（不同门户），而不同的客户端对于表现层的要求有所不同，那么，问题就来了。再者，回到设计层面上分析，从职责单一原则来看，服务层只负责业务，与具体的表现形式无关，因此，它返回的DTO，不应该出现与表现形式的耦合。
理论归理论，这到底还是分析设计层面的思维，是否在实现层面必须这样做呢？一刀切的做法往往会得不偿失，下面我马上会分析应用中如何做出正确的选择。
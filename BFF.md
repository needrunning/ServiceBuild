# BBF概况

 本篇介绍一个概念BFF，Backend-For-Frontend，结合几篇参考文章，从不同的角度理解BFF的发展来源和实际作用。

光说技术，未免有些乏味，技术团队由人组成，技术由人在来选择和使用。我们先从目前互联网技术团队组成的几个 职位工种说起，主要包括前端工程师，node工程师，PHP工程师和后端工程师。前端工程师和node工程师大多隶属前端团队，后端工程师隶属于后端团队，大多更有细分（比如根据业务分为订单，用户，运营支持）。

## 尴尬了 ，PHP工程师属于哪里

从实际情况来看，一但后端团队有java的参与，那么PHP大多不存在或者隶属于前端，他们的职责是调用后端接口，为前端提供一些中转和过度。反过来，一个团队中没有java语言，那么PHP便是真正的后端服务提供语言。如果你说也会有其它语言，比如清一色的go，甚至python，那这种情况不在本篇文章的讨论范围内。

结合下边的这两张图 我们可以找到PHP工程师，当然也包括 node工程师 的定位，那就是
前端页面的数据聚合层，也就是上文 中那个【中转和过度】，往前 连着各个终端，往后对接业务系统暴露的微服务。简化前端页面接入后端服务的 复杂度，根据不同的终端做针对性的 数据适配。

![image.png](https://upload-images.jianshu.io/upload_images/5651-74bd5582a4ce615b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![BFF.png](https://upload-images.jianshu.io/upload_images/5651-a1083d0edcea576b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

注意是第一幅图中的网关层，理论上，网关是微服务体系组成中的重要一环，实际上放到公司技术团队的整个技术架构发展阶段来讲，网关和数据聚合层的粘连和耦合会长期存在，在长期存在的发展过程中，网关的职责会逐步清晰，进而独立成层。

## 端用户体验层->网关层->BFF层->微服务层

在微服务架构中，BFF(Backend for Frontend)也称聚合层或者适配层，它主要承接一个适配角色：将内部复杂的微服务，适配成对各种不同用户体验（无线/Web/H5/第三方等）友好和统一的API。聚合裁剪适配是BFF的主要职责。

1 在微服务架构中，网关专注解决跨横切面逻辑，包括路由、安全、监控和限流熔断等。网关一方面是拆分解耦的利器，同时让开发人员可以专注业务逻辑的实现，达成架构上的关注分离。

2 端用户体验层->网关层->BFF层->微服务层，是现代微服务架构的典型分层方式，这个架构能够灵活应对业务需求的变化，是一种支持创新的演化式架构。

3 技术和业务都在不断变化，架构师要不断调整架构应对这些的变化，BFF和网关都是架构演化的产物。

以上的三点总结出自 [微服务架构：BFF和网关是如何演化出来的？](https://mp.weixin.qq.com/s/EToZ5wqfQCevmgRwdEWdcg)

在没有BFF架构之前，调用接口方式如下图所示，就是根据后端服务的常规调用

![A general purpose API backend.png](https://upload-images.jianshu.io/upload_images/5651-5d0cbdeee67d0388.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 裁剪等个性化诉求催生了BFF

For a mobile API, it's sensible to have a smaller payload footprint and request frequency than a web API

由于客户端类型不同造成了访问接口的诉求不一样，移动端更倾向于较少的请求，较少的数据，以及个性化的数据呈现。

So in practice, our mobile devices will want to make different calls, fewer calls, and will want to display different (and probably less) data than their desktop counterparts.This means that we need to add additional functionality to our API backend to support our mobile interfaces.

>The BFF is tightly coupled to a specific user experience, and will typically be maintained by the same team as the user interface, thereby making it easier to define and adapt the API as the UI requires, while also simplifying process of lining up release of both the client and server components.

这一段主要是说BFF是与前端UI界面，UI UE团队紧密连结在一起的，并且BFF也是由UI，UE团队开发和维护。

![Using one server-side BFF per user interface.png](https://upload-images.jianshu.io/upload_images/5651-cd090b1c2b32baee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 总结

BFF这个词乍一听起来很抽象，实际上离我们并不遥远，技术的发展细化出了很多职位和工种，同时把传统的互联网项目的复杂性大幅度提高了。传统的单体结构的三层抽象也逐步演化成了分布式环境下的端用户体验层->网关层->BFF层->微服务层，多维度的综合体。每一层都在细化和演变。同时在这个变化中，可以感觉到PHP开发者的市场是尴尬和机会并存的。

### 参考阅读

[Pattern: Backends For Frontends](https://samnewman.io/patterns/architectural/bff/)

[bff-soundcloud](https://www.thoughtworks.com/insights/blog/bff-soundcloud)

[微服务架构：BFF和网关是如何演化出来的？](https://mp.weixin.qq.com/s/EToZ5wqfQCevmgRwdEWdcg)

downstream services 下游服务
coupled             联系的，联结的
-----------------------------------

文章已同步到公众号《图南科技》欢迎关注

![图南科技.png](https://upload-images.jianshu.io/upload_images/5651-f9a95406471f320b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

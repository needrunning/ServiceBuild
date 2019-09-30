# 基本概况

针对MongoDB中数据库字段的存储字符长度的疑问，本文采用提出问题假设，描述使用场景，给出对应的接入方案的方式，探讨MongoDB数据建模中字段存储和展示相关的问题，为基于MongoDB的数据库建模提供参考。
## 提出问题

How to improve performance via reduce length of fild in MongoDB
Motivation



MongoDB store BSON document in Memery.For most cases, in application development, you will want to use mongoDB databse,specially storing big data.

These are many ways for impving performance of MongoDB Appliction，  shoud filed shorter and shorter

### 描述

> 1如何合理的进行MongoDB模式下的数据库设计与业务建模？

对MongoDB与关系型数据库在数据建模即数据库设计的深入理解，不断在探索合理的进行数据库设计。既要符合MongoDB数据库的设计规范又要兼顾业务程序和应用设计的便利性，同时又要脱离传统关系型数据库设计的思维局限和思维惯性。

> 2 MongoDB设计规范追求的字段级简模式是否具有实际意义？

基于MongoDB是基于内存的文档数据库，出于节约内存存储的考虑，MongoDB中的集合字段是否应该越短越好。如果字段越短越好那就失去了字段本身的语义化作用。

> 3 如何在统一系统的不同信息调用阶段对于业务字段的长短描述做到平衡

语义化缺失的问题，导致字段描述与其他数据库表字段和程序设计语言中的变量命名规范有冲突。

异构系统接口服务通信时，同一业务实体的字段描述风格之间的转化和平衡问题。

### Example Problem

描述问题

以下图【前后端深度分离】的系统开发模式为例，假设node程序开发的一些功能需要借助MongoDB存储，而其中的部分数据需要借助Java的API接口提供，我们可以理解 Node层也是一个业务层，起到承上启下的作用。也就是我之前文章中提到的BFF层。

![前后端分离.png](https://upload-images.jianshu.io/upload_images/5651-1ff64aec4b8c1bbb.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这一层基于外部接口做业务，业务数据持久化到MongoDB，那么在node程序层面就会出现如何将业务变量的命名字段和MongoDB数据库集合的字段相互对应，转化和存储的问题。


### 前后端深度分离

通常我们有以下几种解决方式

第一种：API接口遵守通用的API接口通信方式，入参采用驼峰命名，返回值采用小写和下划线命名。node采用其本身规范，在MongoDB存储时，程序内部映射为长度较短的key。MongoDb集合中存储为较短字符的字段。

数据结构如下

{

    "_id" : ObjectId("58b95ceea3ebf44aee3bb995"),

    "dt" : ISODate("2017-03-02T00:00:00.000+08:00"),

    "pid" : 440000,

    "prov" : "广东省",

    "etype" : 1,

    "dtime" : ISODate("2017-03-02T02:56:40.000+08:00"),

    "ct" : ISODate("2017-03-03T20:09:15.000+08:00"),

    "edit" : ISODate("2017-03-03T20:09:15.000+08:00"),

}

第二种：对于前端应用本身的数据遵守MongoDB的集合字段极简原则，API数据不考虑转化，直接存储，数据结构如下

{

    "_id" : ObjectId("58b95ceea3ebf44aee3bb995"),

    "dateTime" : ISODate("2017-03-02T00:00:00.000+08:00"),

    "provinceId" : 440000,

    "province" : "广东省",

    "excelType" : 1,

    "dateTime" : ISODate("2017-03-02T02:56:40.000+08:00"),

    "createTime" : ISODate("2017-03-03T20:09:15.000+08:00"),

    "updatetime" : ISODate("2017-03-03T20:09:15.000+08:00"),

}

## 观点输出

My Idea

### 所见即所得

评估系统数量级，保证功能稳定性，简化应用程序开发难度，这种方式也是业界对于MongoDB所见即所得的高开发效率的一种应用，也就是前端传递的字段可以直接毫无转化的存入数据库

MongoDB字段长度有限制吗？
值得注意的是，业界资料，官方文档说明和Mongo社区的线下分享中，关于MongoDB字段的长度规范，都没有特别的作为一个重点指出。而且官方的文档Example中。字段大多是语义化的，下面的数据集结构摘自官方文档。




数据结构
{

  sku: "00e8da9b",

  type: "Audio Album",

  title: "A Love Supreme",

  description: "by John Coltrane",

  asin: "B0000A118M",

  shipping: {

    weight: 6,

    dimensions: {

      width: 10,

      height: 10,

      depth: 1

    },

  },

  pricing: {

    list: 1200,

    retail: 1100,

    savings: 100,

    pct_savings: 8

  },

  details: {

    title: "A Love Supreme [Original Recording Reissued]",

    artist: "John Coltrane",

    genre: [ "Jazz", "General" ],

        ...

    tracks: [

      "A Love Supreme Part I: Acknowledgement",

      "A Love Supreme Part II - Resolution",

      "A Love Supreme, Part III: Pursuance",

      "A Love Supreme, Part IV-Psalm"

    ],

  },

}

在最开始使用MongoDb做系统的很长时间内，我还是倾向于数据库存储字段应该越短越好，并且牺牲字段的语义化。也就是上文提到的解决方案中的第一种。

随着对MongoDb设计思路的理解和使用场景的细致分析，结合应用数据量级，现阶段的我认为 所见即所得，语义化的字段存储并没有明显的劣势。

在MongoDb数据模型设计时，应该被推荐，不需要刻意的强调字段越短越优。参看我之前关于MongoDb的复盘文章

[MongoDB最佳实践系列-几个问题梳理和复盘](https://www.jianshu.com/p/5dba532c8775)

文章已同步到公众号《图南科技》欢迎关注

![MongoDB最佳实践-图南科技](https://upload-images.jianshu.io/upload_images/5651-7678fc0994abb2fd.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/258/format/webp)
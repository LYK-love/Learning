# 需求分析方法

## 需求分析基础

### 为什么要需求分析(需求分析的任务)

• 建⽴**分析模型**，达成开发者和⽤户对需求信息的共同理解。

• 依据共同的理解，发挥**创造性**，创建软件系统解决⽅案。

### 需求分析模型与建模

• “模型是对事物的抽象，帮助⼈们在创建⼀个事物之前可以有更好的理 解”[Blaha2005]

• 建⽴模型的过程被称为建模。“它是对系统进⾏思考和推理的⼀种⽅式。建模的⽬标是<u>建⽴系统的⼀个表示，这个表示以精确⼀致的⽅式描述系统，使得系统的使⽤更加容易</u>”[Fishwick1994]。



建模常用手段:  • `抽象（Abstraction）` • `分解（Decomposition / Partitioning）`

## 面向对象分析

### 用例

* [Jacobson1992] 将⽤例定义为: 在系统(或者⼦系统或者类)和外部对象的**交互**当中所执⾏的⾏为序列的描述,包 括各种不同的序列和**错误的序列**,它们能够**联合提供⼀种有价值的服务**
* [Cockburn2001]认为⽤例描述了在不同条件下<u>系统对某⼀⽤户的请求的响应</u>(就是**交互**)。根据⽤户的请求和请求时的系统条件,系统将执⾏不同的⾏为序列, 每⼀ 个⾏为序列被称为⼀个场景。<u>⼀个⽤例是多个场景的集合</u>



* 按部就班地想到,不要企图一下子想到完整的用例,要先抽象后具体



用例图基本元素:

* ⽤例`Use Case` :
  * Use cases represent typical **sets of scenarios** that help to structure, relate and understand the essential requirements.
  * Express requirements in the form of use cases.
  * Scenarios are descriptions of how a system is used **in practice**
    * Typical **interactions** between a user and a computer system.

* 参与者`actor`: 
  * An `actor`is a **role** that a user or other system plays with respect to the system to be developed.

* 关系 

* 系统边界`System Boundary`:
  * Emphasis the focus on **what is going to be detailed and what is not.**
  * The system boundary is implicitly existent in a diagram without an explicitly represented system boundary.(虽然图标上可能没有范围,实际上隐式地存在着范围)
  * Actors are always <u>outside the boundary</u> and use cases are always <u>inside the boundary</u>.



⽤例图的建⽴:

* ⽬标分析与解决⽅向的确定 
* 寻找参与寻找参与者: 每个⽤户的任务（⽬标）都是⼀个独⽴⽤例
* 寻找⽤例:
  * 
* 细化⽤例:( 如果⽤例的粒度不合适就需要进⾏细化和调整 )
  	判断标准是：⽤例描述了为应对⼀个业务事件，由⼀个⽤户发起，并在⼀ 个连续时间段内完成，可以增加业务价值的任务。
* '''

**常见错误：**

* 不要将⽤例细化为单个操作
  • 例如,不要将⽤户管理细化 为增加、修改和删除三个更⼩的⽤例,因为它们要联合起来 才能体现出业务价值。
* 不要将同⼀个业务⽬标细化为不同⽤例 • 例如特价策略制定和赠送策略制定。
* 不要将没有业务价值的内容作为⽤例
  • 常⻅的错误有“登录”(应该描述为安全性 质量需求)、“数据验证”(应该描述为数据需 求)、“连接数据库”(属性软件内部实 现⽽不是需求)等。

**用例模板：**

| 项目     | 内容描述                                                     |
| -------- | ------------------------------------------------------------ |
| ID       | ⽤例的标识                                                   |
| 名称     | 对⽤例内容的精确描述，体现了⽤例所描述的任务                 |
| 参与者   | 描述系统的参与者和每个参与者的描述系统的参与者和每个参与者的**目标** |
| 触发条件 | 标识启动⽤例的事件，可能是系统外部的事件，也可能是系统内部的 事件，还可能是正常流程的第⼀个步骤 |
| 前置条件 | ⽤例能够正常启动和⼯作的系统状态条件                         |
| 后置条件 | ⽤例执⾏完成后的系统状态条件                                 |
| 正常流程 | 在常⻅和符合预期的条件下，系统与外界的⾏为交互序列           |
| 扩展流程 | ⽤例中可能发⽣的其他场景                                     |
| 特殊需求 | 和⽤例相关的其他特殊需求，尤其是**非功能性**需求             |



## 概念类图（Conceptual Class Diagram）

* ⼜被称为“领域模型”(Domain Model) 
* 类图是⾯向对象分析⽅法的核⼼ 
* 描述类（对象）和这些类（对象）之间的关系
* 与设计类图有所不同
  * 关注系统与外界的交互，⽽不是软件系统的内部构造机制
  * 类型、⽅法、可⻅性等复杂的软件构造细节不会在概念类图中



**建立概念类图：**

* 每个⽤例⽂本描述，尤其是场景描述，建⽴局部的概念类图 
  * 根据⽤例的⽂本描述，识别候选类 
  * 筛选候选类，确定概念类 
  * 识别关联 
  * 识别重要属性
* 将所有⽤例产⽣的局部概念类图进⾏合并，建⽴软件系统的整体概念类图
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
  * 细化用例( 如果⽤例的粒度不合适就需要进⾏细化和调整 )
    	判断标准是：⽤例描述了为应对⼀个业务事件，由⼀个⽤户发起，并在⼀ 个连续时间段内完成，可以增加业务价值的任务。
  * 合并用例
* 细化⽤例
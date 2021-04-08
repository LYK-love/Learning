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

### 建立概念类图

* 对每个⽤例⽂本描述，尤其是场景描述，建⽴局部的概念类图 
  * 根据⽤例的⽂本描述，识别候选类 
  * 筛选候选类，确定概念类 
  * 识别关联 
  * 识别重要属性
* 将所有⽤例产⽣的局部概念类图进⾏合并，建⽴软件系统的整体概念类图

### 候选类识别

* 发现软件系统与外界交互时可能涉及的对象与类，它们就是候选类。 
* ⾏为分析、名词分析、CRC等很多种⽅法都可以⽤来分析⽤例⽂本描述

### 确定概念类的准则

* 依据系统的需求 （ 概念类一定来自现实的需求 ）
* 该类的对象实例的状态与⾏为是否完全必要

### 候选类向概念类的转化

如果候选类的对象实例 

* 既需要维持⼀定的状态，⼜需要依据状态表现⼀定的⾏为 
  * 确定为⼀个概念类
* 如只需要维护状态，不需要表现⾏为 
  * 其他概念类的属性 
* 不需要维护状态，却需要表现⾏为 
  * ⾸先要重新审视需求是否有遗漏，因为没有状态⽀持的对象⽆法表现⾏为
  * 如果确定没有需求的遗漏，就需要剔除该候选类，并将⾏为转交给具备状态⽀持能⼒的其他概念类 
* 既不需要维护状态，⼜不需要表现⾏为 
  * 应该被完全剔除

### 识别关联

* 分析⽤例⽂本描述，发现概念类之间的协作，需要协作的类之间需要建⽴关 联。
* 分析和补充问题域内的关系，例如概念类之间的整体部分关系和明显的语义 联系。
* 对问题域关系的补充要适可⽽⽌，不要把关系搞得过度复杂化。 • 去除冗余关联和导出关联。

### 识别重要属性
* 这些属性往往是实现类协作时必要的信息，是协作的条件、输⼊、结果或者 过程记录。
* 通过分析⽤例的描述，并与⽤户交流，补充问题域信息，可以发现重要的属 性信息。
* 在分析每个单独的⽤例（场景）描述时，为各个概念类发现的重要属性可能 不多，甚⾄有些概念类没有任何重要属性。但是，系统通常有多个⽤例和很 多场景，会建⽴多个局部的概念类图，只有在合并所有局部概念类图之后， 各个概念类的重要属性才能得到全⾯的体现

### 顺序图
* A behavioral model shows the interactions between objects to produce some particular system behavior that is specified as a use-case
* Sequence diagrams (or collaboration diagrams) in the UML are used to model interaction between objects
* 分析阶段，主要是利⽤系统顺序图，表达系统和外部参与者之间的交互⾏ 为。

### Behavioral Diagram —— State Diagram Basic concept

* State: 
  * a set of observable circumstances that characterizes the behavior of a system at a given time
* State transition: 
* * the movement from one state to another
* Event: 
  * an occurrence that causes the system to exhibit some predictable form of behavior
* Action: 
  * process that occurs as a consequence of making a transition

### 建⽴状态图 

* 确定上下⽂环境
  * 状态图是⽴⾜于状态快照进⾏⾏为描述的，因此建⽴状态图时⾸先要搞清楚状态的主体，确定状态的上下⽂环 境。常⻅的状态主体有：类、⽤例、多个⽤例和整个系统。

* 识别状态
  * 状态主体会表现出⼀些稳定的状态，它们需要被识别出来，并且标记出其中的初始状态和结束状态集。在有些情 况下，可能会不存在确定的初始状态和结束状态。
* 建⽴状态转换 
  * 根据需求所描述的系统⾏为，建⽴各个稳定状态之间可能存在的转换。
* 补充详细信息，完善状态图 
  * 添加转换的触发事件、转换⾏为和监护条件等详细信息。



## 结构化分析

结构化分析思想：

* ⾃顶向下分解

* 图 
  * 数据流图
  *  实体关系图 
  * 状态转移图

### Data Flow Diagram ——Flow Oriented Model
* 将系统看做是过程的集合； 
* 过程就是对数据的处理： 
  * 接收输⼊，进⾏数据转换，输出结果
* Represents how data objects are transformed at they move through the system 
* 可能需要和软件系统外的实体尤其是⼈进⾏交互 
* 数据的变化包括： 
  * 被转换、被存储、或者被分布

## Data Flow Diagram —— External Entity
* A producer or consumer of data 
  * Examples: a person, a device, a sensor 
  * Another example: computer-based system
* Data must always originate somewhere and must always be sent to something
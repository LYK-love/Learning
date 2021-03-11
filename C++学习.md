**G = ( VN , VT , P , Z )**

>  VN : `non-terminal`,非终结符号
>
>  VT:终结符号
>
> P:规则
>
> Z：target，目标

高级程序设计语言都是有理论保障的，不然不能保证我们得到正确的结果。



## Programming 

看待程序设计的两个观点：

* The **Science** of programming: 从科学的角度。从这个角度看，许多bug是来自数据流而不是程序本身。
* The **Art** of programming:从艺术的角度。程序设计要时刻注意所处的设计环境。



Von-Neumann structure: 计算器、存储器、控制器、IO

Programming Paradigm

* Procedure:  最经典的就是 程序 = 数据结构 + 算法
* Object-Oriented: OO是对人来说的， 依然在冯诺依曼架构里。
* Functional: 典型的就是 f( g(x) )  =  g( f( x ) ),  在java程序中，如果函数有副作用，那这个式子是不成立的，而函数式就要确保函数没有副作用，这就能满足数学上的表达。这种没有副作用的场景是非常多的，比如说分布式计算就依赖于此
* Logical: 规则 + 条件 → automatic proof










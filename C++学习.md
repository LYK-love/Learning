>  Reference:
>
> > Language:
> >
> > C++ Primer
> >
> > Effective C++
> >
> > More Effective C++
> >
> > Effective Modern C++
>
> > Design:
> >
> > Design Patterns
> >
> > Pattern-oriented Software Architecture



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



## 基本数据类型 built-in datatype

* `char`,`int` , `float` , `double`

* Modifiers: long , short , signed , unsigned

  * `char` 只能用`signed`,`unsigned`修饰
  * `float`不能被修饰
  * `double`只能用`long`修饰
  * `int`可以用四种修饰符组合修饰

* 省略表示

* 操作符`sizeof`

* ANSI C++: `wcchar_t`,`bool`

* typedef

  * 为**已有**的类型定义一个同义词：

  `typedef int INT32;`

  `typedef int A[8];`

## 表达式

* 组成

  * operand
  * operator
  * others

* 求值

  * 优先级

  * 结合性

  * 类型转换约定: 所有计算,规定的都是*同类型*计算. 对于混合运算,我们采取类型转换.有**默认类型转换**( Type Coercion ,  可以查文档) , 也可以强制地改变类型转换约定( Type Casting )( 这可以让你从宽的往窄的地方转, compiler会给一个`warning`,结果你自己负责 ). 我们也可以自己定义各种混合类型的计算.

    * 类型转换是按照计算顺序**逐个**进行的

    * 类型转换精度: 浮点数不能精确表达整数,会有精度损失. 因此`int`默认转成`double`(一定能得到正确答案) 而不是`float`

      

  * 求值次序

    * 取决于Compiler,不是嘴上说说的

    * token:具有独立意义的最小语法单位

    * 代码由编译器翻译为机器码,而编译器中一个重要的功能就是`Optimization`,因此

      `x = 1 + 2 + 3;` 和 `a = 1 + 2 ; x = a + 3` 性能是一样的,所以**没必要为了性能而写出很晦涩的表达式,其实性能都一样**

  * overflow:

    * 加法: 判断结果是否为`0`或者`负数`
    * 减法: 看作加法 ,但是要注意补码特征的问题,如 `min` (`10000...`)取反加一之后还是 `min` 
    * 乘法: 也要注意补码特征问题
    * 除法: 不能除以0.   `-min / -1`有问题,别的都没问题

* 种类

  注意表达式不是语句. `x=1`是表达式,加上**分号**之后`x=1;`才是**表达式语**句. `1`是表达式, `1;`是表达式语句

  * 算数
  * 关系和逻辑
  * 赋值

  * 逗号
  * 字位运算符

* 操作符可重载

  ​	增加语言灵活性. 

  ​	*不是所有操作符都能重载,比如逗号*

  ​	重载后的操作符不能与原来语义相违背,比如`&&`重载后会失去`短路效果`,所以一般不重载`&&`

* 赋值表达式

  *左值 = 右值表达式*

  * 左值: 可以出现在赋值表达式左部的*表达式*,具有存放数据的**确定**地址
  * 类型不同时,先计算右值表达式的值,再转换为左值类型,如`double d = 5/2`,右边会先计算出`2`,然后转为`2.0`

* 算术表达式

  * 增量和简练操作符
    * 前增量(前减量) `++a `     *// 前增量的结果是左值*
    * 后增量(后减量) `--a`
    * 提高编译后的执行效率

* 条件运算符表达式

  * <exp1>?<exp2>:<exp3>

  * 唯一的三目运算符
  * 只计算一个分量
  * 如果<exp2>和<exp2>的值类型相同,且均为左值,则该条件运算符表达式为左值表达式
  * 可嵌套
    * sign(x) `x > 0 ? 1 : x==0? 0 : -1`
    * 就近原则

* 逗号表达式

  * <exp1>,<exp2>,<exp3>...<expn>

  * <expn>的值作为该逗号表达式的值

    ```
    int a,b,c;
    	d = ( a = 1 , b = a + 2 , c = b + 3);
    cout << d << endl; // 6
    ```

  * 如<expn>为左值,则该逗号表达式为左值表达式

* 字位运算符表达式

  * 对整型数二进制位(bit)的操作,将整型数看作二进制序列

  * 与同一个对象异或两次,结果不变( 结合性 )

* 移位运算符表达式

## 语句

* 表达式语句
* IO语句
  * `cin`,`cout`
  * `>>`,`<<`可重载 .   现在它们变成操作符了. `cin<<x`是一个表达式

* 控制流语句

  * 顺序,选择,重复

  * switch是顺序执行的，所以写成`case  1: ... ; case 2:... ;`并没有什么意义,因为`1`和`2`只是个标记,编译器看不懂, 要是写成`case 2:... ;case  1: ... `,就会先执行`2`,再执行`1`.

    

***

* switch的实现与优化: Table_Driven.

  >
  >
  >实现一个哈希表(用枚举),这是一个指针数组。实际上value（就是每条case的地址）是不连续的。但是数组中顺序地存了指向它们的指针，所以逻辑上是连续的。比如两条case的代码地址分别是`08 04 87 f5` `08 04 87 f5`,这是不连续的,设数组起始地址为`08 04 89 e4`,它们分别是前二个元素,那么数组元素的地址分别为`08 04 89 e4` `08 04 89 e8`,我们访问数组的元素,就能连续地间接访问case的代码.

* 表驱动的思想在很多地方都有.

* `Framework`,在C++中是用`宏`完成的(因为这属于编辑`edit`的工作),后来为了简便,用IDE封装了操作

* 函数也是用表驱动的,每个函数都在表里面.注意实现取决于编译器.C的编译器不支持重载,所以`void f(int)`和`void f()`在表中是一个东西,没法作出区分; C++编译器生成的表是把函数签名(而非单纯的函数名)作为表项的(要经过一系列转换),所以上述两个函数是两个不同的表项(签名不同),也就是支持重载.

* 程序中的指令放在`EIP`里. 这是有意义的,因为无论是代码还是数据还是堆区栈区其实都是二进制的,都可以被机器执行,有些恶意代码可以跳转到栈区去,让程序崩溃.因此用了`EIP`,不在其中的指令不能执行,后来有了偷代码的攻击,于是我们把`R+X`也封了,这样小偷就不知道要偷那里的代码.

  ## 函数

* 原则
  * 定义不允许嵌套
  * 先定义后使用
  
* 函数的执行
  * 建立被调用函数的栈空间
  * 参数传递
    * 值传递( call by value )
    * 引用传递( call by reference): reference是别名,所以改变宽宽当然会改变陆昱宽
  * 保存调用函数的运行状态
  * 将控制转交被调函数

所有局部变量一定要初始化才能用,因为栈区不会清零

* 函数原型

  * 遵循先定义后使用原则
  * 自由安排函数定义位置

  * 语句

    

  * 只需参数类型,无需参数名称

  * 编译器检查

* 函数-重载

  * 原则
    * 名同,参数不同(个数,类型,顺序)
    * 返回值类型不作为区别重载函数的依据
  * 匹配原则
    * 严格
    * 内部转换
    * 用户定义的转换 `void f(long); void f(double)`
    * 当产生问题的时候,有可能你的程序逻辑没问题,而是你的相互使用的库有问题

## IO-and-string

### 基本IO

C++ 标准输入输出包含在头文件 <iostream> 中，使用输入输出流库需要引入此头文件
标准库中有 4 个 I/O 相关对象：

* 处理输入的 `istream`对象 `cin`
* 处理输出的 `ostream` 对象 `cout`
* 另外两个 `ostream` 对象 `cerr` 和` clog`

也可以通过引入头文件 `<cstdio>` 或 `<stdio.h>` 使用 `printf` 和 `scanf`

#### 标准输入流cin

* 流提取符 `>>` ,以空白字符或输入结束字符作为终止

  > 输入结束（End-Of-File，EOF）字符：在 Windows 的命令行中，用 `Ctrl + Z` 表示，在类 UNIX 系统的命令行中，用 `Ctrl (Command) + D` 表示

* 读入一个字符

  ```
  char ch ;
  cin.get(ch);
  ```

* 放回一个字符,可能会有问题

  ```
  cin.unget();
  ```

* 删除连续的空白字符:

  `cin >> std::ws;`

  

* 忽略一行中剩余的字符，**丢弃定界符（delimiter）**

  ```c++
  cin.ignore(
      std::numeric_limits<std::streamsize>::max(), 
      '\n'
  ); 
  ```

* 示例:

输入十个数字:

```C++
  int nums[10];
  for( int i = 0 ; i < 10 ; i++ )
  {
  	cin >> nums[i];
  }
```

输入未知个数的数字并求和:

```
  int sum = 0;
  while( cin >> num )
  {
  sum += num;
  }
```

#### 标准输出流cout

* 流插入符`<<`

### 文件I/O

#### < fstream >

* 要在C++进行文件处理,需要引入头文件`<fstream>`

#### < ifstream >类

* 读取文件

  ```C++
  ifstream fin(file_path);
  if (!fin.is_open()) {
      cerr << "file not found" << endl;
  }
  ```


* `ifstream` 的构造函数还可以传入一个 mode 参数，包括但不限于（不同的 mode 可以用按位或运算符 | 组合在一起）：
  * `ios_base::binary` 以二进制方式读取文件
  * `ios_base::app` 在文件末尾追加
  * `ios_base::trunc `丢弃文件中原有的内容

#### < ofstream >类

* 写入文件

  ```C++
  ofstream fout(file_path);
  if (!fin.is_open()) {
      cerr << "file not found" << endl;
  }
  ```

* `ofstream` 的构造函数还可以传入一个 mode 参数，包括但不限于（不同的 mode 可以用按位或运算符 | 组合在一起） ：

  * `ios_base::app` 在文件末尾追加

  * `ios_base::trunc` 丢弃文件中原有的内容

#### < fstream >类

* 兼具 `ifstream` 和 `ofstream` 的功能



  ### 字符串

* 使用 string 需要引入头文件 <string>

* 跟 Java 不同，string 是**可修改内容**的

#### String的相关操作(1) --- IO:

* 读入，以空白字符或 EOF 作为结束标志

  ```
  cin >> s;
  ```

* 读入一行，以**换行符**或**指定的字符**作为结束标志，**丢弃定界符（delimiter）**

```C++
getline(cin, s);       // 以换行符为结束标志
getline(cin, s, ',');  // 以 , 为结束标志
```

#### String的相关操作(1) --- 长度:

* str.size() 和 str.length()，含义相同

* str.capacity() 表示分配的存储空间的大小

* str.empty() 判断 str 是否为空字符串 ""

#### string 的相关操作 (3) – 获取 char

* `str[index]`

  * 0 ≤ index ≤ str.length()

  * index == str.length() 返回末尾的 \0，不应该修改！

* `str.at(int index)`
  * 0 ≤ index ＜ str.length()

* `str.front()`

* `str.back()`

#### string 的相关操作 (4) – 连接

* `s1 = s2 + s3`

* `s1.append(s2)` 或 `s1 += s2`

#### string 的相关操作 (5) – 其他

* 查找

  * str.find("ab"); // 从前向后的第一个 ab

  * str.find("ab", 2); // 从下标 2 开始的第一个 ab

  * str.rfind("ab"); // 从后向前的第一个 ab

  * str.rfind("ab", 2); // 从下标 2 开始从后向前第一次找到 ab

如果找不到，会返回 `string::npos`

#### string 的相关操作 (6) – 与数值互转

* 子串
  * `string s2 = s.substr(pos, n); `// **与** **Java** **不同：**从 pos 开始取 n 个字符

* 比较

  * <、<=、>、>=、==、!=

  * `s1.compare(s2)` 相等时返回 0；s1 < s2 时返回 -1；s1 > s2 时返回 1

* 字符串转换为 int

  * int v = std::stoi(str);

  * 字符串转换为 long、long long、float 和 double 分别为 stol、stoll、stof 和 stod



* 数值转换为字符串
  * string s = std::to_string(42);

#### string 的相关操作 (7) – split (1)

```C++
std::vector<std::string> split(const std::string &s, 
                               const char delimiter) {
    std::vector<std::string> ans;
    std::istringstream iss(s);
    std::string token;
    while (std::getline(iss, token, delimiter)) {
        ans.push_back(token);
    }
    return ans;
}
```

#### string 的相关操作 (7) – split (2)

```c++
std::vector<std::string> split(const std::string &s, const std::string &delim) {
    std::vector<std::string> ans;
    int begin = 0, end = std::string::npos;
    do {
        int end = s.find(delim, begin);
        if (end != std::string::npos) {
            ans.push_back(s.substr(begin));
        } else {
            ans.push_back(s.substr(begin, end - begin));
            begin = end + delim.length();
        }
    } while (end != std::string::pos);
    return ans;
}
```

**注意!** 

* 跟 Java 不同，C++ 的 string **几乎**是一个**字节容器**

```
string s = "中国";

cout << s.length() << endl;
```

输出是4,因为里面是四个字节

* `'\0'`会特殊对待

  ```C++
  char bytes[] = { 
      'a', 'b', 'c', '\0’, 
      'd', 'e', 'f'
  };
  string s(bytes, 0, 7);
  cout << s.length() << endl;
  cout << s << endl;
  ```

   长度是3,输出是`abc`,也就是遇到`\0`会截断

### 命名空间

* `cin` 和 `cout` 是 C++ 标准库内置**对象**而不是关键字

* 标准库的所有标识符都在命名空间 `std` 中

```
using namespace std;  // 直接使用 cin、cout

using std::cin;  // 直接使用 cin、cout，而来自标准库的其他符号需要加上 std:: 前缀
using std::cout; 
```

### 格式化

#### cout格式化输出

* 需要引入头文件 <iomanip>

示例:

* 输出不同进制

  ```
  cout << showbase 
       << hex << 26 << ' ' 
       << oct << 26;
  // 输出：0x1a 032
  ```

* 浮点数输出指定精度

  ```
  cout << setprecision(5) << 3.1415926535;
  // 输出：3.1416
  
  ```

* 输出指定宽度,右对齐

  ```
  cout << setw(6) << right << 10;
  ```

* 输出年月日

  ```
  int year = 2021, month = 3, day = 26;
  cout << year << '-' 
       << setw(2) << setfill('0') << month << '-' 
       << setw(2) << setfill('0') << day;
  // 输出：2021-03-26
  
  ```

* 资源和工具

  •资源

  •https://en.cppreference.com/w/

  •https://zh.cppreference.com/w/%E9%A6%96%E9%A1%B5

  •工具

  •http://cpp.sh/

## Function

* Encapsulation
* Runtime Environment
* Declaration & Definition
  * default parameter
* Overload   Polymorphism

> 0x31 - 0x39 : 1 ~ 10
> 0x41 - 0x5A: A ~ Z
> 0x61 - 0x7A: a ~ z
>
> 0100 0001 ： ‘A'
> 0110 0001 : 'a'
> 可以看到大小写转换只需要反转一个bit，非常方便。 可见ascii表的设计是有考虑的

* inline 内联函数

  * 目的

    * 提高可读性
    * 提高效率

  * 实现方法

    * 编译系统将为inline函数创建一段代码，在调用点，以相应的代码替换

  * 限制

    * 递归
    * 函数指针

    (●'◡'●)适用于：使用频率高、简单、小段代码

  * 一定要在调用它的前面`定义`(而不是仅仅声明)

  * 缺点:

    * 增大目标代码(  object code )
    * 病态的换页( thrashing )
    * 降低指令快取装置的命中率( instruction cache hit rate)

>
>
>### 1、引入 inline 关键字的原因
>
>在 c/c++ 中，为了解决一些频繁调用的小函数大量消耗栈空间（栈内存）的问题，特别的引入了 **inline** 修饰符，表示为内联函数。
>
>栈空间就是指放置程序的局部数据（也就是函数内数据）的内存空间。
>
>在系统下，栈空间是有限的，假如频繁大量的使用就会造成因栈空间不足而导致程序出错的问题，如，函数的死循环递归调用的最终结果就是导致栈内存空间枯竭。
>
>下面我们来看一个例子：
>
>## 实例
>
>```c++
>#include <stdio.h>
> 
>inline const char *num_check(int v)
>{
>    return (v % 2 > 0) ? "奇" : "偶";
>}
> 
>int main(void)
>{
>    int i;
>    for (i = 0; i < 100; i++)
>        printf("%02d   %s\n", i, num_check(i));
>    return 0;
>}
>```
>
>
>
>上面的例子就是标准的内联函数的用法，使用 **inline** 修饰带来的好处我们表面看不出来，其实，在内部的工作就是在每个 **for** 循环的内部任何调用 ***dbtest(i)\*** 的地方都换成了 ***(i%2>0)?"奇":"偶"\***，这样就避免了频繁调用函数对栈内存重复开辟所带来的消耗。
>
>### 2、inline使用限制
>
>**inline** 的使用是有所限制的，inline 只适合函数体内代码简单的涵数使用，不能包含复杂的结构控制语句例如 while、switch，并且不能内联函数本身不能是直接递归函数（即，自己内部还调用自己的函数）。
>
>### 3、inline仅是一个对编译器的建议
>
>**inline** 函数仅仅是一个对编译器的建议，所以最后能否真正内联，看编译器的意思，它如果认为函数不复杂，能在调用点展开，就会真正内联，并不是说声明了内联就会内联，声明内联只是一个建议而已。
>
>### 4、建议 inline 函数的定义放在头文件中
>
>其次，因为内联函数要在调用点展开，所以**编译器必须随处可见内联函数的定义**，要不然就成了非内联函数的调用了。所以，这要求每个调用了内联函数的文件都出现了该**内联函数的定义**。
>
>因此，将**内联函数的定义**放在**头文件**里实现是合适的，省却你为每个文件实现一次的麻烦。
>
>**声明跟定义要一致**：如果在每个文件里都实现一次该内联函数的话，那么，最好保证每个定义都是一样的，否则，将会引起未定义的行为。如果不是每个文件里的定义都一样，那么，编译器展开的是哪一个，那要看具体的编译器而定。所以，最好将**内联函数定义**放在**头文件**中。
>
>### 5、类中的成员函数与inline
>
>**定义**在类中的**成员函数**默认都是**内联的**，如果在类定义时就在类内给出函数定义，那当然最好。如果在类中未给出成员函数定义，而又想内联该函数的话，那在类外要加上 **inline**，否则就认为不是内联的。
>
>```C++
>class A 
>{    
>	public:void Foo(int x, int y) {  } // 自动地成为内联函数 
>}
>```
>
>
>
>将成员函数的定义体放在类声明之中虽然能带来书写上的方便，但不是一种良好的编程风格，上例应该改成：
>
>```c++
>// 头文件 
>class A 
>{    
>	public:    void Foo(int x, int y); 
>	}   
>// 定义文件 
>inline void A::Foo(int x, int y){}
>```
>
>
>
>### 6、inline 是一种"用于实现的关键字"
>
>关键字 **inline** 必须与函数**定义**体放在一起才能使函数成为内联，仅将 **inline** 放在函数声明前面不起任何作用。
>
>如下风格的函数 **Foo** 不能成为内联函数：
>
>```C++
>inline void Foo(int x, int y); // inline 仅与函数声明放在一起
>void Foo(int x, int y){}
>```
>
>而如下风格的函数 **Foo** 则成为内联函数：
>
>```C++
>void Foo(int x, int y);
>inline void Foo(int x, int y) {} // inline 与函数定义体放在一起
>```
>
>所以说，inline 是一种"**用于实现的关键字**"，而不是一种"用于声明的关键字"。一般地，用户可以阅读函数的声明，但是看不到函数的定义。尽管在大多数教科书中内联函数的声明、定义体前面都加了inline 关键字，但我认为**inline不应该出现在函数的声明中**。这个细节虽然不会影响函数的功能，但是体现了高质量C++/C 程序设计风格的一个基本原则：**声明与定义不可混为一谈，用户没有必要、也不应该知道函数是否需要内联。**
>
>### 7、慎用 inline
>
>内联能提高函数的执行效率，为什么不把所有的函数都定义成内联函数？如果所有的函数都是内联函数，还用得着"内联"这个关键字吗？ 
>内联是以**代码膨胀（复制）**为代价，仅仅省去了函数调用的开销，从而提高函数的执行效率。 
>如果执行函数体内代码的时间，相比于函数调用的开销较大，那么效率的收获会很少。另一方面，每一处内联函数的调用都要复制代码，将使程序的总代码量增大，消耗更多的内存空间。
>
>**以下情况不宜使用内联：** 
>（1）如果函数体内的代码**比较长**，使用内联将导致**内存消耗代价较高**。 
>（2）如果函数体内出现**循环**，那么执行函数体内代码的时间要比函数调用的开销大。类的构造函数和析构函数容易让人误解成使用内联更有效。要当心**构造函数和析构函数可能会隐藏一些行为**，如"偷偷地"执行了**基类或成员对象**的构造函数和析构函数。所以**不要随便地将构造函数和析构函数的定义体放在类声明中**。一个好的编译器将会根据函数的定义体，自动地取消不值得的内联（这进一步说明了 inline 不应该出现在函数的声明中）。
>
>### 8、总结
>
>内联函数并不是一个增强性能的灵丹妙药。只有当**函数非常短小**的时候它才能得到我们想要的效果；但是，如果函数并不是很短而且在很多地方都被调用的话，那么将会使得可执行体的体积增大。 
>**最令人烦恼的**还是当**编译器拒绝内联**的时候。在老的实现中，结果很不尽人意，虽然在新的实现中有很大的改善，但是仍然还是不那么完善的。一些编译器能够足够的聪明来指出哪些函数可以内联哪些不能，但是大多数编译器就不那么聪明了，因此这就需要我们的经验来判断。**如果内联函数不能增强性能，就避免使用它！**

## 程序组织

* 程序结构
  * 逻辑结构
  * 物理结构
    * 多个源文件组成
    * `main`唯一
  * 工程文件
    * 外部函数
    * 外部变量

> 所谓静态链接是指把要调用的函数或者过程链接到可执行文件中，成为可执行文件的一部分。换句话说，函数和过程的代码就在程序的exe文件中，该文件包含了运行时所需的全部代码。当多个程序都调用相同函数时，内存中就会存在这个函数的多个拷贝，这样就浪费了宝贵的内存资源。
>    动态链接所调用的函数代码并没有被拷贝到应用程序的可执行文件中去，而是仅仅在其中加入了所调用函数的描述信息（往往是一些重定位信息）。仅当应用程序被装入内存开始运行时，在Windows的管理下，才在应用程序与相应的DLL之间建立链接关系。当要执行所调用DLL中的函数时，根据链接产生的重定位信息，Windows才转去执行DLL中相应的函数代码

创建一个`a.h`

```C++
//"a.h"

extern float salary;
extern void show();

static int count = 0; //不加static是程序级的,加了static就变成文件级的,这样就不会冲突了
float salary = 0;
static void process() // static表明这个process的作用域是文件级的
{
	
}
```

```c++
//"b.cpp"
#include "a.h"

const double pi = 3.14; //写了const不会有冲突(因为编译器没有必要为了这个常量保留一个符号表,在link的时候添加,常量在本文件内就被替换了),因为是字面常量,就是说,对于const而言默认是文件级. 可以把所有常量放在一个 const.h 中

static int count = 0;
static void process()
{
    salary = 100;
    
}

```

### 头文件:

* 常量定义
* 变量/函数声明
* 编译预处理
* 类型定义
* 内联函数

### namespace

* 理念
  * 兼容
    * link时不冲突
    * 程序中定义新名字时不必担心与其他(比如库)冲突
    * 在库里增加名字,不影响用户
    * 不同库里含有同名元素,可选择
    * 不修改函数的前提下,可消解名冲突
    * 避免名字空间的名字之间发生冲突
    * 使名字空间可以处理标准库
* 快速( 设计者的理念,要让人在见到这个新特性的时候要很快地理解 )
  * 

* 两种形式

  *  declaration:

    ```
    
    ```

  * directive

不建议在同一文件内两次使用directive

* Cpp
* 
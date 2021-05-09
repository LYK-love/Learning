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

* `int stoi(string)` : 把字符串转换成整数

#### 标准输出流cout

* 流插入符`<<`

### 文件I/O

#### < fstream >

* 要在C++进行文件处理,需要引入头文件`<fstream>`

#### < ifstream >

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

#### < ofstream >

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

#### < fstream >

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

#### 命名空间

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



## 程序组织

* 逻辑结构
* 物理结构
  * 多个源文件组成
  * main唯一
* 工程文件
  * 外部文件
  * 外部变量

### namespace

### 编译预处理

* 与作用域, 类型, 接口等概念格格不入
  * 潜伏于环境
  * 穿透于作用域

#### #include

  * make interface definitions available
  * compose source text

#### #define

  * Symbolic constants    `const`
  * Open subroutines `inline`
  * Generic subroutines  `template` //这三种复用都是源代码层次的，即 可以看到细节的
  * Generic "types"  `template`
  * Renaming  `namespace`   // 以上五点，C++中已经有了替换的方法，而下面三点，C++中还没有合适的替代方法：
  * String concatenation
  * Special purpose syntax
  * General macro processing

  ```C++
  # define MAX(x,y) x >= y ? x : y //不加括号的后果
  12 * MAX(2,3)
      12 * 2 >= 3 ? 2 : 3
  
  
  
  
  # define MIN(x,y) ((x) < (y) ? (x) : ( y));//这样可以实现泛型，前提是类类里面重载了“<”运算符
  
  ```

  缺点：

  * 重复计算，因为宏不是函数
  * 没有类型检查，太宽松了

  注意：

```c++
#define ADD(x,y) {x+y;}
int x=0,y=1;
if( x == 0 )
    ADD(x,y);  //会报错,因为花括号后面有分号
else
    cout << "HI";
//但如果写成:
#define ADD(x,y) x+y;
cout << ADD(x+y) << endl; //会报错
//只能写成:
#define ADD(x,y)  do{ x + y ; } while(0);
```



  #### 选择性编译

* version  control

```C++
# ifndef MY_PRINT_VERSION
	#define MY_PRINT_VERSION 1
# endif

# if MY_PRINTF_VERSION == 1
void printf( char *str )
{ ... }

#elif MY_PRINTF_VERSION == 2
int printf( char *fmt , char *args,... )
{ ... }
#endif
```

* Commenting out code

  #### #pragma

* Control of layout
* Informing the compiler

##  数组

* 特征

  * 相同类型
  * 连续存储

* 一维数组

  * 类型定义

  * 函数接口

    * 元素个数须通过参数**显式**给出, 不能通过`sizeof`取得. 

      传入的`len`不能保证真的是数组长度,C++是允许数组越界的

      * 字符串

```C++
void  f( int a[16] )
{
	int len = sizeof(a);  //这是错误的
}
//必须写成:
void  f( int a[16] , int size)			
```

``` c++
char s1[] = "abc"; // == char s1 = {'a','b', 'c','\0'}
char s2[] = {'a','b', 'c' };
```

```C++
//找到arr中的第一个负数
#include<iterator>
int arr[] = {0,1,2,3,4,5.-1};
int *pbeg = begin(arr), *pend = end(arr);
while( pbeg!= pend && *pend  >= 0)
	++pbeg;
```

### 删除所有数组所有元素

```
int remove(int * arr, int target, int n){
	int front = 0, back = 0, targetCnt = 0;
	for(; back < n; back++){
		if(arr[back] == target){
			targetCnt++;
		}else{
			arr[front] = arr[back];
			front++;
		}
	}
	return targetCnt;
}



int main(int argc, char const *argv[])
{
	int a1[] = {1, 2, 3, 4, 0, 6, 6, 6, 7, 8, 6, 4, 5};
	int l1 = 1;

	l1 -= remove(a1, 6, l1);

	for(int i = 0; i < l1; i++){
		std::cout << a1[i] << " ";
	}
	std::cout << std::endl;
	system("pause");
	return 0;
}

```



### 多维数组

* 定义
* 存储组织,C++中一定要知道数组的`layout`(内存布局). C++中的多维数组只是一维数组的不断迭代,和java中的容器等是不一样的
* 参数传递
  * 缺省第一维( C++里没有`ragged array`)

```C++
int arr[][3] = {{1} , {2,3} , {4,5,6} }
cout << arr[0][1] << endl; //java中这会报错,但是C++中这是允许的,会得到一个未定义的值. 1的后面是两个未定义的值,再往后是2,3和一个未定义的值,然后是4,5,6. 也就是说真的有3 * 3 = 9 个元素. 这和java中的ragged array不同.
```

* 升/降维处理

## Struct

* 赋值 --- 同类型
*  alignment. 契合硬件,提升效率
* 参数传递

```C++
struct B
{
    char b; //1
    int a; //4
    short c; //2
};
cout << sizeof(B) << endl; //答案是12,因为会对齐
```

## union

* 共享存储空间

  ```C++
  union C
  {
  	char b; //1
  	int a; //4
  	short c; //2
  };
  cout << sizeof(C) << endl; //答案是4
  ```

  ```C++
  union Matrix
  {
  	struct 
  	{
  		double a11, a12, a13;
  		double a21, a22, a23;
  		double a31, a32, a33;
  	};
  	double _element[3][3];
  };	
  
  Matrix m;
  	int i, j;
  	for (i = 0; i < 3; i++)
  		for (j = 0; j < 3; j++)
  			m._element[i][j] = (i + 1) * (j + 1);
  
  	m.a11 = 0;
  	m.a22 = 0;
  	m.a33 = 0;
  
  	for (i = 0; i < 3; i++)
  		for (j = 0; j < 3; j++)
  			cout << m._element[i][j] << endl;
  ```

  

## 指针

* 管理地址信息
* 调用代码

### 指针定义与基本操作

* 用`typedef` 定义一个指针类型

  `typedef int* Pointer;`

  `pointer p,q` // p, q均为指针变量

  注意: 指针其实不是一个类型,所以`  int *p,q `中, q不是指针

* 赋值

  `int *p = (int*) 0xKN231232`  现在没人用这个了

* 操作符

  `&`取地址

  `*`间接取内容

  注意: C++中, `NULL`是`0`; 

  * ANSI C: #define NULL( (void*) 0 )   (用 ((void\*)0)来置换NULL,这种方式有很大漏洞 )

    C++: #define NULL 0 ( 即用 0 去置换NULL )

  *空指针并不一定用与整数0同样的二进制模式表示,可由实现者采用任何选定的方式表示*

  * 现在空指针都用`nullptr`赋值

* 同类型指针比较

* 输出

  * 特例: 原因是操作符重载

    ```C++
    char *p = "ABCD";
    cout << p; //p指向的字符串,即"ABCD"
    cout << *p; // p指向的字符,即'A'
    //对于int*之类的就不会这样
    ```

* 例: 将某块内存清零

  ```C++
  void memset( void *pointer, unsigned size )
  {
      char *p = (char*) pointer;//必须要类型转换,不然p是void的指针,无法进行操作
      for( int k = 0 ; k < size ; k++ )
          *p++ = 0; 
      
  }
  ```

  

* 常量指针与指针常量

  * **常量指针**, 即 指针指向一个常量. ( 也可以指向一个变量, 但指针不知道.所以常量指针就是一个**只读的指针**,可以**消除函数副作用** )

    ```C++
    const  int c = 0;
    const int *cp;
    
    int y = 1;
    int *q;
    
    cp = &c;
    q = &y;
    *cp = 1; // 不行,指针还没有绑定
    *q = 2;
    cp = &y; //可以,常量指针可以指向一个变量,这样的用法非常常见,不能通过指针来修改y,只能用y来修改y
    q = &c;// 不可以. 变量指针不能指向一个常量
    //如果硬要让变量指针指向常量,可以用 const_cast<int>,这种方法不太好:
    //假设你有一个 const A a = 8; 你需要把a传入一个 
    // void fun( A *x) 中,如果你确保fun不会更改a的话,那可以在传参的时候写 fun( const_cast<A *>&a ).
    //这是在函数给定的情况下的被逼无耐之举, 有条件的话,应该把fun写成 void fun( const A *x)
    // 没事干不要用 const_cast<>
    
    ```

    * **常量替换**在编译期间发生,类似于宏替换.

      ```C++
      const int a = 5;
      
      int *p = (int *)&a; //让p指向与a相同的内存空间
      cout << &a << ", " << p << endl;
      *p = 10; // 照说a的值也应该改变，实际却没有,这就是常量折叠.
      cout << a << ", " << *p << endl;
      // 这个"常量折叠"就是在编译器进行语法分析的时候，将常量表达式计算求值，并用求得的值来替换表达式，放入常量表。可以算作一种编译优化。
      // 我只是改了这个地址内容,但是a还是5,
      // 因为编译器在优化的过程中，会把碰见的const全部以内容替换掉
      // （跟宏似的: #define PI 3.1415,用到PI时就用.1415代替），
      // 这个出现在预编译阶段；但是在运行阶段，它的内存里存的东西确实改变了!!!
      // 简单来说就是, 常量a的内存空间里面的内容在运行期间会被更改为10, 但是编译器在预编译阶段,已经用a的值(这个时候a的值还是5) 来替换a这个名字,类似于宏替换. 所以a这个名字的值永远是5,但它代表的内存空间的值可能被改变.
      
      输出是:
      0x61fe14, 0x61fe14
      5, 10
      ```

      

    * **常量指针**,就是说指针本身是一个常量, 因此必须在定义的时候初始化.

      `<类型> * const <指针变量>`

    * 数组的最后一个元素的后一个元素的指针是空指针`nullptr`

### 指针数组

* main函数:

  ```C++
  int main( int argc, char* argv[], char* env[] )
  {
      cout << argc << endl;
      for( int i=0; i != argc ; i++ )
      {
          cout << argv[i] << endl;
      }
  
        cout << env << endl;
  
        return 0;
  
    }
  ```

  `argc`:参数个数

  `argv`:命令行参数

  `env`:环境参数

  

### 多级指针

* 编写一个函数，交换两个字符串

  ```C++
  int main( int argc, char* argv[], char* env[] )
  {
      char *p1 = "abcd";
      char *p2 = "1234";
      cout << p1 << "  " << p2 << endl;
      swap( &p1, &p2 );
      cout << p1 << "  " << p2 << endl;
      return 0;
  
  
    }
  ```

  

### 动态变量

* 申请(当然是堆区)
  * `new <类型名>`
  * `new <类型名> [ <整形表达式> ]`
  * `new`和`malloc`都能申请堆区内存. 当为类的对象分配内存时,`new`会执行构造函数,而`malloc`只会申请内存,不会执行构造函数. 因此C++中尽量用`new`而不是`malloc`
  * 申请内存也有可能失败. 因此对于内存申请,一定要判断是否成功,即异常处理
* 归还
  * 操作符
    * `new` --- `delete`  会调用析构函数
    * `delete []`
    * 申请的指针,不要改变它的值,这是因为申请空间使用的是`cookie`的方式. 如果硬要改变,那得创建一个副本,然后更改副本. 总之,不能更改申请的指针

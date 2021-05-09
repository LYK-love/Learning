# 面向对象

面向对象的优势是可以`设计`出`可复用性`和`可维护性`更强的代码. OO和PO能做的事其实是一样的,OO甚至会更慢,因为多态必然造成性能的下降.

**OO只是设计层面的思想,和运行没有关系**

1. 弱耦合性: 代码更容易复用
2. 容易维护,主要是因为继承和多态,不点的接口,多种行为,类的内部可以自由修改(只要不该接口)

例子:

* PO实现Stack:

```c++
#include<iostream>
using namespace std;
#define STACK_SIZE 100
struct Stack
{
    int top;
    int buffer[STACK_SIZE];
};

bool push( Stack &s , int i )
{
    if( s.top == STACK_SIZE - 1 )
    {
        cout << "stack is overflow!" << endl;
        return false;
    }
    else
    {
        s.top++;
        s.buffer[s.top] = i;
        return true;
    }
}

bool pop( Stack &s, int &i )
{
    if( s.top == -1 )
    {
        cout << "stack is empty" << endl;
        return false;
    }
    else
    {
        i = s.buffer[s.top];
        s.top--;
        return true;
    }
}

int main()
{
    Stack st1,st2;
    st1.top = -1;
    st2.top = -1;
    int x;
    push( st1,12 );
    pop( st1,x );
    cout << x << endl;
    return 0;
}
```

* OO实现Stack

  ```c++
  #include<iostream>
  using namespace std;
  #define STACK_SIZE 100
  
  class Stack
  {
      private:
      int top;
      int buffer[STACK_SIZE];
      public:
      Stack() {top =  -1 ;}
      bool push( int i );
      bool pop( int &i );
  };
  
  bool Stack::push( int i )
  {
   if( top == STACK_SIZE - 1 )
      {
          cout << "stack is overflow!" << endl;
          return false;
      }
      else
      {
          top++;
          buffer[top] = i;
          return true;
      }
  
  }
  bool Stack::pop( int &i )
  {
      if( top == -1 )
      {
          cout << "stack is empty" << endl;
          return false;
      }
      else
      {
          i = buffer[top];
          top--;
          return true;
      }
  }
  
  int main( void )
  {
      Stack st1,st2;
      int x;
      st1.push(12);
      st1.pop(x);
      cout << x << endl;
      return 0;
  }
  ```

  

C++ 成员函数都有一个隐含的`T *const this`,指向本对象( 也就是存储的是本对象的地址 )

* `getter`和`setter` 可以在类定义时定义,这样它们就成为`隐式内联函数`

## 成员初始化表

* 构造函数的补充
* 执行
  * **先于构造函数体**
  * **按类数据成员申明次序**

```C++
Class A
{
	int x;
	const int y;
	int &z;
	public:
		A():y(1),z(x),x(0) //先于构造函数体,按类数据成员声明顺序,所以x初始化为0,z引用x. 再x赋值为10,z也变为10.
			{ x = 100 }
};
```

成员初始化表: 构造函数在分配内存的时候直接用这个值来进行初始化

`x = 100`: 这是赋值,不是初始化. 构造函数先初始化x,然后复制为100.

* 在构造函数中尽量使用成员初始化取代赋值动作
  * `const`成员, `reference`成员, `对象成员`
  * 效率高
  * 数据成员太多时,不采用本条准则
    * 降低可维护性



**例题**

```C++
class CString
{
	char *p;
	int size;
public:
CString(int x): size(x), p(new char[size]) {}

};
```

错了! 因为p初始化的时候,`size`还没有初始化! 应该把`size`声明提前

## 析构函数

* `~<类名>()`
* 对象消亡时,系统自动调用( 释放对象持有的非内存资源和不属于这个对象的内存 )
* RAII vs GC:  
  * RAII: `Resource Accuisition Is Installization` 资源获取即初始化
  * 获得了一个资源,就像对待对象一样对待它

* `public`
  * 可定义为`private`

```

```

### `Const`成员

* `const`成员

  * `const`成员变量

  ```C++
  class A
  {
  	const int x;
      public
  		A( int i)
  		:x( i )
  		{
  		;
  		}
  };
  ```

  * 初始化放在构造函数的**初始化表**中进行
  * `static const`: 类静态常量,这个常量放在`静态区`,只能在类定义时初始化(而不是在构造函数内, 因为它不从属于某个对象)

### 静态成员

* 问题:同一个类的不同对象如何共享变量

* 

  ```C++
  class A
  {
  	int x,y;
  	static int shared;
  	
  	public:
  		static void f();//静态成员函数,只能存取静态成员变量, 遵循类访问控制
  		void q();
  
  };
  
  int A::shared = 0; //在函数定义的时候不需要写static; 不在构造函数内初始化
  void A::f()
  {
  	;
  }
  ```

  

* 静态成员的使用

  * 通过对象使用

    `A a; a.f();`

  * 通过类使用(不像某些语言一样用`A.f()`)

    `A::F()` 

* 单例:

  ```
  ```

## 友元

在使用C++进行项目开发的过程中难免会使用友元及前置声明 下面就对它们进行讲解：

在此之前，先来了解下什么是友元函数？什么是友元类？什么是友元成员函数？为什么需要友元？

友元函数是指某些虽然不是类成员的函数却能够访问类的所有成员。友元类同理，只是友元类与友元函数最主要的区别是：一个是将某个函数作为类的友元，一个则是将整个类（所有成员函数）都作为其他类的友元。而友元成员函数顾名思义就是将某个类的某个成员函数作为其他类的友元。一般情况下，非成员函数是无法直接从外部访问类的私有或保护部分的，但是在有些开发中又需要非成员函数从外部访问该类的私有或保护部分，而友元可以实现。

类的友元函数：

```C++
class Base{
private:
    int Num;
public:
    Base(int n = 0):Num(n){}
    void setValue(int n){Num = n;}
    void show()const{std::cout << "BaseNum:" << Num << std::endl;}
    friend void setData(Base&,int);     //声明友元函数
};

void setData(Base& s1,int n){
    s1.Num = n;   //#1 可以直接访问
}
```



如果没有 `friend void setData(Base&,int)`;该行声明语句的话，类外部函数`setData`是无法访问类私有成员`Num`的，当有该行友元声明的话，`setData`函数将可以直接访问该类的私有部分`Num`成员，如代码中#1所示，这是编译器所允许的。
友元**类**：

```C++
class Base1;    //前置声明 因为Base1类在Base类后面定义的，而Base类提到了Base1类(声明友元类的时候)
                //所以必须让编译器知道有这个类 也可以省略该步 但是在声明友元类的时候应该这样写：
friend class Base1;
class Base
{
private:
    int Num;
public:
    Base(int n = 0):Num(n){}
    void setValue(int n){Num = n;}    //设置一个自定义新值
    void clearValue(){Num = 0;}       //将值置为0
    void show()const{std::cout << "BaseNum:" << Num << std::endl;}
    friend Base1;   //将Base1整个类作为该类(Base)的友元 即Base1的所有成员函数均是Base类的友元
};

class Base1
{
public:
    void setData(Base& s1,int n){s1.Num = n;}     //与Base::setValue函数功能相同 使用了友元特性
    void clearData(Base& s1){s1.clearValue();}    //与Base::clearValue函数功能相同 但没有使用到友元特性
};
```



当需要将一个类的所有成员函数作为另一个类的友元的话，可以将这个类直接作为另一个类的友元，这样整个类的成员函数都将是另外一个类的友员。如上面代码所示，因此Base1类中的`setData`和`clearData`函数都是Base类的友元，都可以直接从外部对Base类的私有或保护成员进行操作。因为Base1类在Base类后面定义的，在编译friend Base1;这句代码的时候，编译器并不知道Base1是个什么东西，所以必须在将Base1类放在Base类前面定义或者在Base类前面进行前置声明，上面代码正是这么做的。`class Base1;`这行代码就是前置声明。那么对于上面代码有没有其他方法可以省略前置声明并实现同样效果呢？答案是肯定的，在这里可以省略前置声明，但是必须要将friend Base1;改为friend class Base1;这样编译器就知道将Base1是一个类，然后将它设为友元。

有人可能会问了，能不能将Base1放在Base前面定义，然后前置声明一个class Base;呢？可以，但是必须要将Base1的函数定义部分去掉。如下所示：

```C++
class Base;    //对Base的前置声明 

class Base1{
public:
    void setData(Base& s1,int n);    //在这里不能定义函数
    void clearData(Base& s1);        //同上
};

class Base{
private:
    int Num;
public:
    Base(int n = 0):Num(n){}
    void setValue(int n){Num = n;}
    void clearValue(){Num = 0;}
    void show()const{std::cout << "BaseNum:" << Num << std::endl;}
    friend Base1;    //在此之前 编译器已经知道了Base1的完整定义 所以不用再对Base1进行前置声明
};

void Base1::setData(Base& s1,int n){
    s1.Num = n;
}

void Base1::clearData(Base& s1){
    s1.clearValue();
}
```




为什么不能在类中定义该函数呢？因为如果在Base1中定义了`setData`和`clearData`函数，而函数体中对Base类的成员进行操作了，这样就必须事先知道Base**类的完整定义**(让编译器知道类内部情况)，不然编译器<u>不知道Base类中有没有这些成员</u>，所以不允许这么做。但是能不能在类中定义`setData`和`clearData`函数并在Base1类前面进行前置声明Base类解决这个问题呢？不行！因为前置声明顾名思义只是提前声明，前置声明class Base;只是让编译器知道，有这么一个Base类将在后面进行定义，但是编译器并不知道该类的内部情况，所以编译器只允许在知道该**类的完整定义**后，才让对该类成员进行操作(就是定义对这个类的成员进行操作的函数)，否则不允许。( 所以不能定义函数,只能声明函数 )
到这里，相信聪明的你应该发现，Base1类中只有函数`setData`使用了友元特性，对Base类私有成员直接访问。而`clearData`函数的实现只是调用了Base类的公有方法`clearValue`，间接访问私有成员，但是这并不涉及到友元特性。所以这个函数没有必要成为Base类的友元。如果一个类中有几十个函数，而大部分都没有使用到友元特性，将他们都设置为友元的方法（即友元类）并不推荐，而只有当大部分成员函数都需要使用友元特性的时候，使用友元类将非常方便，而只有个别的成员函数涉及到友元特性的话，推荐使用下面这个友元方法，但是这种方法需要特别注意类的定义顺序。

友元**成员函数**：

```C++
class Base;    //对Base的前置声明 

class Base1{
public:
    void setData(Base& s1,int n);    //在这里不能定义函数
    void clearData(Base& s1);        //同上
};

class Base{
private:
    int Num;
public:
    Base(int n = 0):Num(n){}
    void setValue(int n){Num = n;}
    void clearValue(){Num = 0;}
    void show()const{std::cout << "BaseNum:" << Num << std::endl;}
    friend void Base1::setData(Base& s1,int n);    //声明友元成员函数
};

void Base1::setData(Base& s1,int n){
    s1.Num = n;
}

void Base1::clearData(Base& s1){
    s1.clearValue();
}
```

在声明友元类的时候，只要不在类内部定义函数，顺序无关紧要，只要添加后面定义的类的前置声明就好了。而友元成员函数就不行，因为在使用`friend void Base1::setData(Base& s1,int n);`这句代码进行声明友元成员函数的时候，提到了Base1**类的成员函数**，既然需要将这个类的`setData`函数设为友元，那么就必须提前知道Base1类的**完整定义**(了解类的内部情况)，那么就必须将Base1类放在Base类的前面进行定义，以便当编译器编译`friend void Base1::setData(Base& s1,int n);`这行代码的时候就已经知道Base1类的内部情况了，所以定义的顺序也至关重要，而且Base1类中的函数不能在类中定义，因为定义了的话，就需要知道Base的内部情况(类完整定义)那么就需要将Base放在Base1前面定义，而Base又需要将Base1放在Base前面，这将相互矛盾，所以最友善的解决方法就是Base1的函数不在类中定义，这也是至关重要的。

* 如果**类B提到了类A的成员函数,**那么需要提前知道类A的完整定义.
* 如果**类B的成员函数提到了类A**,那么只需要前置声明A.而B的函数定义要写在A的**类定义**后面

另外，使用前置声明时，例如将Base1放在Base前面定义，并且使用前置声明`class Base;`那么在Base1类成员部分中不能实例化Base类对象，因为实例化也涉及到构造函数，需要让编译器知道Base类的完整定义，使用前置声明`class Base;`是不行的！要么Base1类中不进行实例化Base类，要么就在Base1类成员部分定义一个Base类的指针，并且在Base1类**构造函数**中对该指针使用`new Base;`方法实例化，这样是可以的，因为只定义Base类指针，不需要了解Base类内部情况，只需要知道Base是一个什么类型就好了，如前面的前置声明class Base;就让编译器知道了，Base是一个类，而`Base*`是一个Base类的指针。如下代码：



```C++
class Base;    //对Base的前置声明 

class Base1{
public:
    void setData(Base& s1,int n);    //在这里不能定义函数
    void clearData(Base& s1);        //同上
    Base1(int n = 0);
private:
//      Base temp;         //error! 需要在此之前知道Base的完整定义
        Base* pTemp;       //OK! 只需要提前知道Base是什么类型就好了 前面class Base;已经告诉编译器
};

class Base{
private:
    int Num;
public:
    Base(int n = 0):Num(n){}
    void setValue(int n){Num = n;}
    void clearValue(){Num = 0;}
    void show()const{std::cout << "BaseNum:" << Num << std::endl;}
    friend void Base1::setData(Base& s1,int n);    //声明友元成员函数
};

void Base1::setData(Base& s1,int n){
    s1.Num = n;
}

void Base1::clearData(Base& s1){
    s1.clearValue();
}

Base1::Base1(int n){
    pTemp = new Base(n);     //实例化Base类
}

在C++中还有模版友元 这将在后面讲述。有些人可能会问了，C++友元会不会与面向对象思想相悖？不会！因为友元只能由类定义，例如需要将Base1声明为Base类的友元，那么就只能在Base类中进行声明，而不能在外部强加友情，因此，尽管友元被授予从外部访问类的私有部分和保护部分的权限，但他们并不与面向对象编程思想相悖，相反，他们提高了公有接口的灵活性。

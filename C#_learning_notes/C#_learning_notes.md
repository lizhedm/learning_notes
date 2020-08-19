### Quick overview

#### Program structure 程序结构

- 没有分开的头文件和源文件，全部代码都放在.cs文件中

- 程序入口在Main函数 (attention:M is capital)

- C#中的一切都封装在类中，类被打包到namespace命名空间中

- 定义类或者结构体完成的右括号 **'' } ''** 后面不需要 **'' ; ''** (C++ 需要)



#### Namespaces 命名空间

通过using namespace,来在另一个namespace中使用前一个namespace中包含的class

```c#
using system;
namespace exampleNameSpace{
    class exampleClass{
        public void exampleFunc(){
            //	do something
        }
    }
}
```

```c#
using system;
using exampleNameSpace;
namespace doSomethingNameSpace{
    class doSomethingClass{
        public void Main(string[] args){
            exampleClass ex = new exampleClass();
            ex.exampleFunc();
        }
    }
}
```



C#中using 对应替代了C++中#include的功能



#### Variables

- C# 中没有global variables全局变量和全局函数，通过static variables和static functions来达到同样的效果
- 访问变量前都需要initialize



#### Data types 数据类型

- C#中有一些基本数据类型的内存长度和C++的不一样长，涉及到考虑数据内存长度的代码时需要关注和注意
- 用户自定义的数据类型:
  - Class
  - Struct
  - Interface
- C#有<u>垃圾回收</u>机制，new创建的object不需要delete
- struct在比较轻量的复合变量情况下使用，如果复合变量太复杂则需要用class



##### 内存分配

- value types分配在stack栈中
  - 除string外的所有built-in types
  - Struct
  - Enum
- reference types分配在heap堆中，由垃圾回收机制管理
  - Class
  - Interface
  - Collection types like Array
  - String



#### Operators and expressions



#### Enumerations



```c#
enum Weekdays{
    Sunday,Monday,Tuesday,Wednesday,Thursday,Friday,Saturday
}
```





#### Statements







#### Classes and structs







#### Modifiers

- public, protected, private
- readonly
  - 只在class成员变量中使用，修饰只读变量，不可修改
  - 和const的区别是const变量必须在声明处初始化，readonly可以不在声明处初始化

- sealed

  - 盖章密封，修饰的class不能被其他class继承

    ```c#
    sealed class NoOneCanInheriteMe{
        ...;
    }
    ```

- unsafe

  - 用于需要在工程中添加不安全代码的情景，例如C++的指针	

    ```C#
    public unsafe ExampleFunc(){
        int[] exampleArray = new int[10];
        for(int i = 0;i < exampleArray.Length;i++){
            exampleArray[i] = i;
        }
        fixed(int* pExaArr = exampleArray)
        //	C#中使用C++指针操作数组，用fixed固定指针指向，指向不可更改
        for(int i = 0;i < exampleArray.Length;i++){
            System.Console.WriteLine(pExaArr[i]);
        }
    }
    ```

  - unsafe 也可以单独将代码块包裹

    ```c#
    unsafe{
        public ExampleFunc(){
            ...;
        }
    }
    ```

    
  

#### Properties

get方法和set方法

```c#
using system
Class Date{
    public int Day{
        get {
            return day;
        }
        set {
            day = value;
            //	value是个特殊的关键字，只在属性访问器set中使用，表示要将属性设置的值
        }
    }
    int day;
    ...
}
```





#### Interfaces 接口

C# 没有C++中的多类继承 multiple class inheritance

C# 中多继承通过Interface来实现 



##### 定义

接口：包含一组虚方法的抽象类型，每一种方法都有名称、参数和返回值。但是没有任何实现

```C#
public interface System.IComparable{
    int CompareTo(object o);
}

public class TestCls: IComparable{
    public TestCls(){
    
    }

    private int _value;
    public int Value{
        get { return _value; }
        set { _value = value; }
    }

   public int CompareTo(object o){
        //	使用as模式进行转型判断
        TestCls aCls = o as TestCls;
        if (aCls != null){
        	//	实现抽象方法
        	return _value.CompareTo(aCls._value);
        }
    }
}
```





#### Abstract Class 抽象类

##### 定义

- 抽象类提供多个派生类共享基类的公共定义，它既可以提供抽象方法，也可以提供非抽象方法

- 抽象类不能实例化，必须通过继承由派生类实现其抽象方法， 因此对抽象类不能使用new关键字，也不能被密封

- 如果派生类没有实现所有的抽象方法，则该派生类也必须声明为抽象类

- 实现抽象方法由 override来实现

  

```C#
abstract public class Animal{
    //	定义静态字段
    static protected int _id; 
    //	定义属性
    public abstract static int Id{
        get;
        set;
    }

    public abstract void Eat();

    //	索引器
    public string this[int i]{
        get;
        set;
    } 
}
```

```c#
public class Dog: Animal{
    public static override int Id{
        get {return _id;}
        set {_id = value;}
    }

    public override void Eat(){
        Console.Write("Dog Eats.")
    }
}
```



#### 接口和抽象类对比

##### 相同点

- 都不能被直接实例化，都可以通过继承实现其抽象方法
- 都是面向抽象编程的技术基础，实现了诸多的设计模式



##### 不同点

- 接口支持多继承，抽象类不能实现多继承
- 接口只能定义抽象规则；抽象类既可以定义规则，还可能提供已实现的成员
- 接口是一组行为规范；抽象类是一个不完全的类
- 接口可以用于支持回调；抽象类不能实现回调，因为继承不支持
- 接口只包含方法、属性、索引器、事件的签名，但不能定义字段和包含实现的方法；抽象类可以定义字段、属性、包含有实现的方法
- 接口可以作用于值类型和引用类型；抽象类只能作用于引用类型。例如，Struct就可以继承接口，而不能继承类



#### Function parameters

##### By-Value/In parameters

参数以值的方式传入函数内部，传递的是值得拷贝，函数中值被改变，函数外这个值是不变的



##### By Reference/In-Out parameters

参数以指针pointer或者引用reference的方式传入函数内部，传递的是地址，函数中值被改变，函数外这个值也会被改变1

<u>在使用之前必须赋初始值</u>，不能传递一个未初始化的reference参数进入函数

C# 使用关键字 **ref**

```c#
void ExampleFunc(ref int exampleValue){
    ...;
}

int exampleValue = 1;
ExampleFunc(ref exampleValue);
```



##### Out parameters

<u>在使用完返回时必须赋值</u>

函数只有一个返回值，需要输出多个值时，可以使用out参数

```C#
int GetValueA(out int valueB){
    int a;
    int b;
    ...;	//	do something about a and b
    valueA = a;
    valueB = b;
    return valueA;
}
```



##### Params 参数数组

- 用于修饰方法的参数，只能修饰一维数组

- 一个方法只能有一个params参数数组，切位于函数参数项最后，不能有默认值

- 调用函数时，可以传参数数组，也可以分开传数组各元素

  ```c#
  ExampleFunc(string param1,params int[] paramsArray){
      ...;
  }
  
  int[] paramsArray = new int[]{1,2,3,4,5,6};
  string strParam = "test";
  ExampleFunc(strParam,paramsArray);	//	传参数数组
  ExampleFunc(strParam,7,8,9);	//	传数组各元素
  ```

  



#### Arrays

C# 中数组访问越界是非法的，会被编译器检测报错。

语法差异：

- [] 放在类型后，而不是变量后

  ```C#
  //	C# style
  int[] arrayCSharp = new int[10];
  
  //	C++ style
  int arrayCPlusPlus[] = new int[10];
  ```

- C# 支持多维数组和 jagged数组

  ```c#
  //	2 dimensional
  int[,] array2D = new int[2,3]
      
  //	3 dimensional
  int[,,] array3D = new int[2,3,4]
      
  //	jagged array
  int[][] arrayJagged = new int[3][]
  arrayJagged[0] = new int[2]{1,2};
  arrayJagged[1] = new int[5]{3,4,5,6,7}
  arrayJagged[2] = new int[3]{8,9,10};
  ```

- 多维数组和jagged数组的区别

  - 多维数组的大小是N*M规则矩形

  - jagged锯齿数组的大小设置灵活，在锯齿数组中，每一行都可以有不同的大小



#### Indexers 索引器

使用 **this** 关键字，指向对象实例

```c#
static public int size = 10;
private string[] namelist = new string[size];
public string this[int index]{
    get{
        return namelist[index];
    }
    set{
        namelist[index] = value;
    }
}
```



Indexer可以重载，除了整型，也可以是其他类型如string

```C#
static public int size = 10;
private string[] namelist = new string[size];
public string this[int index]{
    ...;
}

public int this[string name]{
    get{
        for(int i=0; i < size; i++){
            if(namelist[i] == name){
                return i;
            } 
        }
    }
}
```





#### Boxing and unboxing

C# 中的所有数据类型都来自object类

将一个变量instance包裹进object称为boxing，将包裹在object中的变量instance取出称为unboxing

```c#
int exampleInt = 10;
object objBox = exampleInt	//boxing
int unboxInt = (int) objBox;	//unboxing
```



#### Delegates



#### Inheritance and polymorphism



### UIH C# 编码规范

#### Code Review Example

![](resource\code_review_1.png)

![](resource\code_review_2.png)

#### Reference

> Clean Code 代码整洁之道
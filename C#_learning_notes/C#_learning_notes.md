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



#### Data types

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

  - 

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





#### Interfaces

C# 没有C++中的多类继承 multiple class inheritance

C# 中多继承通过Interface来实现 



#### Function parameters



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
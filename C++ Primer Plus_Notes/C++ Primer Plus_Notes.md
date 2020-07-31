## 语法

**泛型（generic programming）**: 创建独立于类型的代码



**变量使用前需要做声明的优点**：拼写错误的变量名使用会被编译器检测到



**C++变量声明位置**：首次使用变量之前声明它



**auto声明关键字**: 编译器按照初始值类型推断变量类型 

不能将数组赋值给另一个数组（其他语言编码习惯可能造成影响，需注意），string类型可以赋值给另一个string



**指针的初始化**：一定要在解除引用运算符（*）前，将指针初始化为一个确定的适当的地址。



**动态内存分配注意事项**：

1. new 和 delete是成对的
2. 不要使用delete释放不是new分配的内存
3. 同一内存，不要delete两次
4. new[] 为数组分配内存，对应使用delete[]释放 



**变量存储**

1. 自动存储：函数内部定义，存储在栈中
2. 静态存储：
   - static
   - 函数外定义
3. 动态存储：new delete，存储在堆中



**数组、vector、array**

数据和array存储在栈中

vector存储在堆中

```c++
double a1[4] = {1.2, 3.4, 5.6, 7.8};

vector<double> a2(4);

array<double,4> a3  = {1.2, 3.4, 5.6, 7.8};
```



**i++ and ++i**

i++：使用i当前值计算表达式，得到结果+1

++i：先将i+1，然后用新的i值计算表达式结果



#### for 循环



基于范围的for循环

```c++
for (double x:prices)
//	prices is a array    
```



#### 函数相关



**函数的地址**

函数名就是函数的地址



**函数指针**

```c++
//	function:
double example(int);

//	function pointer:
double (*pExample)(int);	//	pExample points to a function that taks one int argument and returns double type
```



##### 函数重载（函数多态）

使用不同的参数列表实现

默认参数



**函数模板**：泛型编程

```c++
template <typename exampleType>
void ExampleFunc(exampleType &a,exampleType &b){
    exampleType temp;
    temp = a;
    a = b;
    b = temp;
}
```



##### 函数实例化和具体化



**显式具体化（explicit specialization）**

提供具体化函数定义

```c++
//	job is a type
template <> void ExampleFunc<job>(job &a,job &b){
    ...;
}
```



**隐式实例化（implicit instantiation）**

```c++
ExampleFunc(i,j);
//	函数调用ExampleFunc(i,j)，编译器生成函数调用ExampleFunc()的int类型实例
```



**显示实例化（explicit instantiation）**

```c++
//	使用ExampleFunc()模板生成int类型的函数定义
template void ExampleFunc<int>(int,int);
```



## UIH C++编码规范

### 定义和缩略语/Definition and Abbreviation

除变量/形参 外使用Pascal命名法：每一个单词的首字母都采用大写字母

```c++
void FirstNameFunc(){
    ...;
}
```



### 描述/Description

#### 通用规则

##### 面向对象

避免使用C语言的语法,e.g.

- std::string	~~char~~
- new delete 	~~malloc free~~



##### 避免简单的复制粘贴代码

附带的问题不可控不可预期



##### 通用的资源管理

- 需要使用时再分配资源，不再使用需及时释放

- 资源指 内存、文件句柄、socket和端口、数据库连接、锁和光标等

- 尽晚分配，尽早释放

- 涉及到分配资源时做异常处理

  ```C++
  try{
      //	allocate resource
  }
  catch(Exception){
      //	handle exception
  }
  ```



##### 通用的内存分配

- 避免使用全局变量，可使用全局函数或者静态成员函数返回全局变量

  ```c++
  class FileSystem{...};
  
  FileSystem TFS(){
  	static FileSystem theFileSystem;
      return theFileSystem;
  }
  ```

- 自己申请的内存自己负责释放，不要期望其他人之后完成释放的工作

- <span style ="color:red"> 如果内存是内部分配的，需要提供额外的方法来释放内存。避免一个动态库分配的内存在另一个动态库中释放带来的问题。</span>

- 避免比较指针，除判断是否为空外

  ```c#
  if(NULL == p)
  //	== 判断语句变量放在右边，防止错误赋值操作
  ```

- 释放数组时，使用delete[]

  ```C++
  delete[] p;	//	p points to an array
  p = NULL;
  ```

- 释放完内存，将指针赋值为空

- 使用智能指针，避免内存泄漏

  - unique_ptr	同一时间内只有一个智能指针可以指向该对象
  - shared_ptr 多个智能指针可以指向相同对象，最后一个引用注销时释放资源
  - weak_ptr 不控制对象生命周期，从一个shared_ptr或者另一个weak_ptr构造，其构造和析构不会造成引用计数增减。

- 在循环体外声明变量

- 不要在栈上放大量数据，用堆来分配大的数据

  ```c++
  ExampleClass exaArray[10000];	//	stack,wrong
  
  std::unique_ptr<ExampleClass[]> pExaArray(new ExampleClass[10000])	//	heap,right
  ```

  

  











### 参考reference

> [1] Effective C++ [1] 3rd Edition
>
> [2] C++ Coding Standards: 101 Rules, Guidelines and Best Practices, SutterHerb Sutter , et.al et.al et.al.
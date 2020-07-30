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


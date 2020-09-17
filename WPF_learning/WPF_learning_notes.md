## WPF: A Beginner's Guide 

### Layout

**Panel类控件**：Canvas，DockPanel，Grid，TabPanel,ToolBarOverflowPanel，StackPanel，ToolBarPanel，UniformGrid，VirtualizingPanel，VirtualizingStackPanel,WrapPanel

Margin：四个值的顺序，左开始，顺时针

#### DockPanel

泊靠式面板。内部元素可以选择泊靠方式。

- DockPanel.Dock，value：Left/Right/Top/Bottom

- LastChildFill=True 最后一个内容控件填充所有剩余部分

#### Grid

- 行高与列宽可以使用绝对值，相对比以及最大值和最小值
- 内部元素可以设置自己的所在列和行，还可以设置自己跨几列和行。
---

- Grid.Column 值表示从整个Grid 分列的第几列开始占据，列的范围从0开始计数。后面的列可以覆盖前面列的界面。
- Grid.Row一样

---

- Grid.ColumnSpan 表示占据Grid 的列数，最小为1
- Grid.RowSpan一样



#### WarpPanel

自动折行面板。当一行元素排满后会自动换行。类似html中的流式布局。

#### StackPanel

内部元素在纵向或者横向上紧密排列，形成栈式布局。

- Orientation：Horizontal，Vertical
- HorizontalAlignment 内部元素水平方向上的对齐方式。value：Left，Center，Right，Stretch。
- VerticalAlignment 内部元素竖直方向上的对齐方式。value：Top，Center，Bottom，Stretch。



### TBD

#### To do in XAML

- 表示UI的markup
- 需要的resource 文件 
- 本地resource文件
- Command Binding

#### To do in Code

- event handling
- non-UI class methods
- exception handling

### Resource

#### Dynamic Resources 和 Static Resource

静态资源在第一次编译后即确定其对象或值，之后不能对其进行修改。动态资源则是在运行时决定，当运行过程中真正需要时，才到资源目标中查找其值。



#### C#代码中使用资源

- FindResource 查找资源
- Resource.Add 增加资源
- Resource.Remove 移除资源



### RoutedEvents and RoutedCommands

---

#### WPF内置路由事件

- 冒泡：由事件源向上传递一直到根元素

- 直接：只有事件源才有机会响应事件

- 隧道：从元素树的根部调用事件处理程序并依次向下深入直到事件源



#### Command

**命令(Command)**：实现了`ICommand`接口的类. 常用的即`RoutedCommand`

**命令源(Command Source)**：命令的发送者，是实现了`ICommandSource`接口的类

**命令目标(Command Target)**：命令发送给谁，命令作用在谁的身上。命令目标必须是实现了`IInputElement`接口的类

**命令关联(Command Binding)**：负责把一些外围逻辑和命令关联起来，比如执行之前对命令是否可以执行进行判断、命令执行之后还有哪些后续工作等。



### Dependency Property

依赖属性（Dependency Property）: 自己没有值，能通过Binding从数据源获得值（依赖在别人身上）的属性，用于依赖属性的对象被称为依赖对象

依赖对象 : WPF允许对象在创建时，不包含各个字段所占用的空间，而在使用这个字段时通过其他对象的数据或者实时分配空间，这种对象就是依赖对象

### Binding

---

![picture_5_1](resource\picture_5_1.png)

**four components:**

- a binding target object, 绑定目标对象
- a **target property**, 绑定目标属性
- a binding source, 绑定源
- a path to the value in the binding source to use, 路径

**target property** 必须是依赖属性 `Dependency Property`

WPF的Binding中`Path`必须是CLR属性



**Binding.Mode：**

- `OneWay` : `source property`改变  —> `target property`改变,`target property`改变 —> `source property`不改变，适用于只读的control
- `TwoWay` ：`source property`和 `target property`双向改变，适用于可编辑和交互的UI
- `OneTime` `source property`初始化 `target property`，后续更改不会传播
- `OneWayToSource` ：`OneWay`的反向属性
- `Default` 

source must implement a suitable property change notification mechanism such as `INotifyPropertyChanged`



**Binding.UpdateSourceTrigger：**

`UpdateSourceTrigger` property of the binding determines what triggers the update of the source.

| UpdateSourceTrigger value                | When the Source Value Gets Updated        |
| ---------------------------------------- | ----------------------------------------- |
| `LostFocus` (default for `TextBox.Text`) | When the `TextBox` control loses focus    |
| `PropertyChanged`                        | As you type into the `TextBox`            |
| `Explicit`                               | When the application calls `UpdateSource` |



**Databinding Syntax:**

```xaml
<TextBox x:Name="txtSource" Width="150" Height="30"/>
<TextBox Width="150" Height="30" Text="{Binding ElementName=txtSource, 
    Path=Text, Mode=TwoWay, UpdateSourceTrigger=LostFocus }"/>
```

```xaml
<TextBox Width="150" Height="30" Text="{Binding Text}"/>
```



 `Binding` was a markup `MarkupExtension`. XAML parser knows how to treat the { } sections

```xaml
<Button Margin="10,0,0,0" Content="Im bound to btnSource, using long Binding syntax">
    <Button.Background>
        <Binding ElementName="btnSource" Path="Background"/>
    </Button.Background>
</Button>
```





## Other

数据驱动UI: 传统的GUI界面都是由windows消息通过事件传递给程序，程序根据不同的操作来表达出不同的数据体现在UI界面上，这样数据在某种程度上来说，受到很大的限制。WPF中是数据驱动UI，数据是核心，处于主动的，UI从属于数据并表达数据，是被动的.
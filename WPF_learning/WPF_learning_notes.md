## WPF: A Beginner's Guide - Part 1，2,3,4,5 of n

### Layout

**Panel类控件**：Canvas，DockPanel，Grid，TabPanel,ToolBarOverflowPanel，StackPanel，ToolBarPanel，UniformGrid，VirtualizingPanel，VirtualizingStackPanel,WrapPanel

Margin：四个值的顺序，左开始，顺时针

#### DockPanel

泊靠式面板。内部元素可以选择泊靠方式。

常用布局：menu在上，左右内容显示区域，底部一个状态显示栏。

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

### Resource

#### Dynamic Resources 和 Static Resource

静态资源在第一次编译后即确定其对象或值，之后不能对其进行修改。动态资源则是在运行时决定，当运行过程中真正需要时，才到资源目标中查找其值。



#### C#代码中使用资源

- FindResource 查找资源
- Resource.Add 增加资源
- Resource.Remove 移除资源

## Other

数据驱动UI: 传统的GUI界面都是由windows消息通过事件传递给程序，程序根据不同的操作来表达出不同的数据体现在UI界面上，这样数据在某种程度上来说，受到很大的限制。WPF中是数据驱动UI，数据是核心，处于主动的，UI从属于数据并表达数据，是被动的.
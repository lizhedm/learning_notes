### Button Command

#### 绑定Button Command带参数

```xaml
<!--xaml绑定（带参/不带参）-->
<Button Command="{Binding CancelCommand}"/>
<Button Command="{Binding CancelCommand}" CommandParameter="something"/>
```

```c#
public ICommand CancelCommand => new DelegateCommand(Cancel);
        private void Cancel(object commandParameter)
        {
            //...
        }
```

> reference: LinkSettingDemo code



### DOM操作

#### 获取控件父控件

```c#
public T GetParentObject<T>(DependencyObject obj, string name) where T : FrameworkElement
{
    DependencyObject parent = VisualTreeHelper.GetParent(obj);
    while (parent != null)
    {
        if (parent is T && (((T)parent).Name == name | string.IsNullOrEmpty(name)))
        {
            return (T)parent;
        }
    	parent = VisualTreeHelper.GetParent(parent);
    }
    return null;
}
```

> reference: LinkSettingDemo



#### 获取控件内所有子控件

```C#
List<T> FindVisualChild<T>(DependencyObject obj) where T : DependencyObject
{
    try
    {
        List<T> list = new List<T>();
        for (int i = 0; i < VisualTreeHelper.GetChildrenCount(obj); i++)
        {
            DependencyObject child = VisualTreeHelper.GetChild(obj, i);
            if (child is T)
            {
                list.Add((T)child);
                List<T> childOfChildren = FindVisualChild<T>(child);
                if (childOfChildren != null)
                {
                    list.AddRange(childOfChildren);
                }
            }
            else
            {
                List<T> childOfChildren = FindVisualChild<T>(child);
                if (childOfChildren != null)
                {
                    list.AddRange(childOfChildren);
                }
            }
        }

        return list;
    }
    catch (Exception)
    {
        //MessageBox.Show(ee.Message);
        return null;
    }
}
```

> reference: LinkSettingDemo



### 算法

#### 集合中删除和复原添加回连续的子集

```c#
Collection2.ForEach(item =>
            {
                if (item.Category == categoty && item.Level == BrainRegionLevel.SecondLevel && item.IsSearchHit)
                {
                    item.IsShow = isShow;
                }
            });
if (!isShow)
            {
    			//	delete
                for(int index = Collection1.Count -1; index > 0; index--)
                {
                    if (!Collection1[index].IsShow)
                    {
                        Collection1.RemoveAt(index);
                    }
                }
            }
            else
            {
                //	insert
                int count = Collection2.Count;
                for (int index2 = 0,index1 = 0;index2 < count && index1 < count; index2++)
                {
                    if (index1 >= Collection1.Count)
                    {
                        if (Collection2[index2].IsShow)
                        {
                            Collection1.Insert(indindex1ex, Collection2[index2]);
                            index1++;
                        }
                        continue;
                    }
                    if (Collection2[index2] == Collection1[index1])
                    {
                        index1++;
                        continue;
                    }
                    if (Collection2[index2].IsShow)
                    {
                        Collection1.Insert(index, Collection2[index2]);
                        index1++;
                    }
                }
            }
```

> reference McsfBrainAnalysis
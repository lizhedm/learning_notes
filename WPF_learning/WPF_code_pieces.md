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
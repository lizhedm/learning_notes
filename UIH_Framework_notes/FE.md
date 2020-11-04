### FE

#### 层级

入口 `FE.xml`

![image_1](D:\Git\learning_notes\UIH_Framework_notes\image\image_1.png)



调试的`log`输出设置

![image_2](D:\Git\learning_notes\UIH_Framework_notes\image\image_2.png)



配置进入`Container.config` 和`MainModelContainer.xml`

![image_3](D:\Git\learning_notes\UIH_Framework_notes\image\image_3.png)



`Container` : 完成应用配置然后传给 `Common` 

`ModelContainer` :  接口对应的实现部分



#### AppPreInitializer

传入应用名称、当前通信节点、所用UI资源等内容

```c#
public interface IAppPreInitializer
    {
        void Initialize(string appName, FrameworkElement rootUI, ICommunicationProxy proxy);
    }
```



#### AppInitializer

进行一些基本初始化，包括对`CommunicationModuleModel`、`AppCommandHandlerModel`、`AppEventHandlerModel`的初始化以及注册`Handler`等

```c#
public interface IAppInitializer
    {
        void Initialize(IModelContainer container, string appName, FrameworkElement rootUI, ICommunicationProxy proxy);
    }
```





#### Container.config

`Macrosoft Unity` : 一个轻量级AOP框架，提供构造注入、拦截注入、属性注入、方法注入。



`<container>` 标签中注册应用的资源

资源类型：

- Models
- Workflow, Workstep
- ViewModels
  - Command ViewModels
  - `Save` Command ViewModels
- Panel Operation
- Cell Operation
- Cell Initialize Item
- Cell Control Creator



#### MainModelContainer.xml

```xml
<Root>
    <Models>
    </Models>
    
    <ViewModels>
    </ViewModels>
</Root>
```



配置 `UI` 资源：

```xml
<Item Name="UIResourceModel" MapToClassName="UIResourceModel" Keep="true" Path="brainanalysis/config/FE/UIResource.xml"/>
```



配置 `快捷键` 绑定：

```xml
<Item Name="InputBindingModel" MapToClassName="InputBindingModel" Keep="false" Path="brainanalysis/config/FE/InputBinding.xml"/>
```



其他主要配置：

|           Name           |           Class            |         File Name         |
| :----------------------: | :------------------------: | :-----------------------: |
| `AppCommandHandlerModel` |  `AppCommandHandlerModel`  |    CommandHanlder.xml     |
|  `AppEventHandlerModel`  |   `AppEventHandlerModel`   |     EventHandler.xml      |
|      `AllFunction`       | `ControlAssemblyViewModel` |      AllFunction.xml      |
|       `WorkStep1`        | `ControlAssemblyViewModel` |       WorkStep1.xml       |
|       `WorkStep2`        | `ControlAssemblyViewModel` |       WorkStep2.xml       |
|    `GeneralFunction`     | `ControlAssemblyViewModel` |    GeneralFunction.xml    |
|      `ExitFunction`      | `ControlAssemblyViewModel` |     ExitFunction.xml      |
|      `CommonTools`       | `ControlAssemblyViewModel` |      CommonTools.xml      |
| `TissueROIControlTools`  | `ControlAssemblyViewModel` | TissueROIControlTools.xml |
|   `TissueROIDrawTools`   | `ControlAssemblyViewModel` |  TissueROIDrawTools.xml   |
|                          |                            |                           |
|                          |                            |                           |
|                          |                            |                           |
|                          |                            |                           |
|                          |                            |                           |
|                          |                            |                           |
|                          |                            |                           |
|                          |                            |                           |
|                          |                            |                           |



#### 依赖注入 Dependency Injection

把耦合从代码中移出去，放到统一的XML文件中，通过一个容器 **`Container`** 在需要的时候把这个依赖关系形成，即把需要的接口实现注入到需要它的类中。
### FE

#### 层级

入口 `FE.xml`

![image_1](D:\Git\learning_notes\UIH_Framework_notes\image\image_1.png)



调试的`log`输出设置

![image_2](D:\Git\learning_notes\UIH_Framework_notes\image\image_2.png)



配置进入`Container.config` 和`MainModelContainer.xml`

![image_3](D:\Git\learning_notes\UIH_Framework_notes\image\image_3.png)



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
|      `AllFunction`       |  ControlAssemblyViewModel  |      AllFunction.xml      |
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


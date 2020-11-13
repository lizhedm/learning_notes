# BE

## 层级



![BE_image_1](D:\Git\learning_notes\UIH_Framework_notes\image\BE_image_1.png)



```mermaid
graph TD;
BEEntry[BEEntry.xml];
LC[LibraryCollection.xml];
WFX[WorkflowController.xml];
Lib1[xxx.dll];
Lib2[xxx.dll];
Lib3[... .dll];

BEEntry-->LC;
BEEntry-->WFX;
LC-->Lib1;
LC-->Lib2;
LC-->Lib3;
```

## WorkflowController.xml

```mermaid
graph LR;
WFC[WorkflowController.xml];
CH[Command Handler];
EH[Event Handler];
OP[Operation];
WF[Workflow.xml];
TM([Thread Model]);
DD([DisplayDelegate]);
style DD stroke:color:#fff,stroke-dasharray: 5 5
style TM stroke:color:#fff,stroke-dasharray: 5 5

WFC-->TM;
WFC-->CH;
WFC-->EH;
WFC-->WF;
WFC-->OP;
WFC-->DD;

```

### CommandHandler

```xml
  <AppCmdHandler ID="10002">AppPluginCommonCellOperationCmdHandler</AppCmdHandler>
  <AppCmdHandler ID="10003">AppPluginCommonCmdHandlerLoadSeries</AppCmdHandler>
  <AppCmdHandler ID="10004">AppPluginCommonCtrollerOperationCmdHandler</AppCmdHandler>
  <AppCmdHandler ID="12008">AppPluginCommonPanelOperationCmdHandler</AppCmdHandler>
  <AppCmdHandler ID="15107">AppPluginCommonCmdHandlerLoadSeries</AppCmdHandler>
  <AppCmdHandler ID="1416">AppPluginCommonCmdHandlerLoadSeries</AppCmdHandler>
```





### EventHandler

```xml
  <!-- Event handler -->
  <AppEventHandler ChannelID="11"  EventID="20005">AppPluginCommonMedviewerBasisConfigEventHandler</AppEventHandler>
  <AppEventHandler ChannelID="11"  EventID="20007">AppPluginMMPresetWindowLevelConfigEventHandler</AppEventHandler>
  
  <!-- Leave and Enter App Event handler -->
  <AppEventHandler ChannelID="9"   EventID="151001">BrainAnalysisEnterAppEventHandler</AppEventHandler>
  <AppEventHandler ChannelID="9"   EventID="151002">AppPluginCommonLeaveAppEventHandler</AppEventHandler>
```



```mermaid
graph TB;
McsfAppPlugin-->AppPluginCommonMedviewerBasisConfigEventHandler;

McsfAppPluginMMCommon-->AppPluginMMPresetWindowLevelConfigEventHandler;
```





### Operation

![BE_image_2](D:\Git\learning_notes\UIH_Framework_notes\image\BE_image_2.png)





## Workflow

```mermaid
graph LR;
WF[Workflow];
WS[workstep];
AC[AppCell];
AM[AppModel];

DS[DisplayStep];
RS[RegistStep];
AS[AnalysisStep];

WF-->WS;
WF-->AC;
WF-->AM;
WS-->DS;
WS-->RS;
WS-->AS;
```

### AppModel

应用后端的数据模型



### AppCell

相当于应用后端的`view`

脑分析将AppCell统一放在`LayoutList.xml`中



![BE_image_3](D:\Git\learning_notes\UIH_Framework_notes\image\BE_image_3.png)

![BE_image_4](D:\Git\learning_notes\UIH_Framework_notes\image\BE_image_4.png)

![BE_image_5](D:\Git\learning_notes\UIH_Framework_notes\image\BE_image_5.png)



### workstep

```mermaid
graph LR;
WS[workstep];
OP[Operation];
PI[PanelInfo];
WS-->OP;
WS-->PI;
```




### 总结

后端框架实际上可以视为采用了MVC模式

**M** (`AppModel`)

**V** (`AppCell`)  `MedViewer`

**C** (`workstep`)



## Diagram

![BE_image_6](D:\Git\learning_notes\UIH_Framework_notes\image\BE_image_6.png)



## 线程模型

![BE_image_7](D:\Git\learning_notes\UIH_Framework_notes\image\BE_image_7.png)



线程1和线程2，红色方框内的部分，两个线程之间是加锁的；

线程2 在`AppResult Merge`的时候和线程3 `DisplayDelegateInvoke`时，两个线程是加锁的。
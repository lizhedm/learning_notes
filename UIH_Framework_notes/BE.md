# BE

## 层级



![BE_image_1](D:\Git\learning_notes\UIH_Framework_notes\image\BE_image_1.png)



```mermaid
graph TD;
BEEntry[BEEntry.xml]
-->LC[LibraryCollection.xml];
BEEntry[BEEntry.xml]-->WFX[WorkflowController.xml];
LC-->Lib1[xxx.dll];
LC-->Lib2[xxx.dll];
LC-->Lib3[....dll];
```


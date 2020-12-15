# Code Pieces



拿到Volume

```c++
auto spVolume = spMultiVolume->GetVolume(sVolumeUID);
```



判断数据模态

```c++
if(spVolume->GetDataPackage()->GetModality() == AppModality::CT)
```


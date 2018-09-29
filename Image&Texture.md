# Image&Texture
## Load Data from File
### Check File Exist
> ```c++
>FString InFileName;
>```
```c++
#include "PlatformFilemanager.h"
```
```c++
FPlatformFileManager::Get().GetPlatformFile().FileExists(*InFileName)
```
### Load Data to TArray from File
>```c++
>TArray<uint8> InData;
>```
```c++
FFileHelper::LoadFileToArray(InData, *InFileName)
```
## Parse Format
### Module Manager
```c++
#include "ModuleManager.h"
```
### Load IImageWrapperModule
```c++
#include "ImageWrapper/Public/IImageWrapperModule.h"
#include "ImageWrapper/Public/IImageWrapper.h"
```
```c++
IImageWrapperModule& ImageWrapperModule = FModuleManager::LoadModuleChecked<IImageWrapperModule>(FName("ImageWrapper"));
```
### IImageWrapper

```c++
IImageWrapperPtr ImageWrapper = ImageWrapperModule.CreateImageWrapper(EImageFormat::PNG);
```
> Or
```c++
TSharedPtr<IImageWrapper> ImageWrapper = ImageWrapperModule.CreateImageWrapper(EImageFormat::PNG);
```
### Data
```c++
ImageWrapper->SetCompressed(InData.GetData(),LoadData.Num())
ImageWrapper->GetRaw(ERGBFormat::RGBA,8,Data)
```
> ```c++
> int32 Width, Height;
> ```
```c++
Height = ImageWrapper->GetHeight();
Width = ImageWrapper->GetWidth();
```

## Save
```c++
ImageWrapper->SetRaw(Data->GetData(),Data->Num(),Width,Height,ERGBFormat::RGBA,8)
OutData = ImageWrapper->GetCompressed()
```
```c++
#include "FileManagerGeneric.h"
#include "Paths.h"
```
```c++
FFileManagerGeneric::Get().DirectoryExists(*OutFile)
```
```c++
FFileManagerGeneric::Get().MakeDirectory(*FPaths::GetPath(OutFile), true)
```
```c++
FFileHelper::SaveArrayToFile(OutData, *OutFile)
```


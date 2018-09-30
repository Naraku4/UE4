# Image&Texture
## Load Data from File
### Check File Exist
```c++
#include "PlatformFilemanager.h"
```
> ```c++
>FString InFileName;
>```
```c++
FPlatformFileManager::Get().GetPlatformFile().FileExists(*InFileName)
```
### Load Data to TArray from File
```c++
#include "FileHelper.h"
```
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
```
```c++
IImageWrapperModule& ImageWrapperModule = FModuleManager::LoadModuleChecked<IImageWrapperModule>(FName("ImageWrapper"));
```
### IImageWrapper
```c++
#include "ImageWrapper/Public/IImageWrapper.h"
```
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
```
>```c++
>TArray<uint8> InData;
>```
```c++
OutData = ImageWrapper->GetCompressed()
```
```c++
#include "FileManagerGeneric.h"
```
```c++
FFileManagerGeneric::Get().DirectoryExists(*OutFile)
```
```c++
#include "Paths.h"
```
```c++
FFileManagerGeneric::Get().MakeDirectory(*FPaths::GetPath(OutFile), true)
```
```c++
FFileHelper::SaveArrayToFile(OutData, *OutFile)
```


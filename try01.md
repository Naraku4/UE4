
插入代码:
``` c++
USTRUCT(BlueprintType)
struct FData_PageInfo
{
    GENERATED_USTRUCT_BODY()

    FData_PageInfo();
    FData_PageInfo(UChildActorComponent *parent_Com);

    void reInit();

    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "struct_Variants")
        class UChildActorComponent *Parent_Com;

    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "struct_Variants")
        class ACpp_PagerActor *PageActor;

    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "struct_Variants")
        class UChildActorComponent *FrontCanvas_Com;

    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "struct_Variants")
        class UChildActorComponent *BackCanvas_Com;
};
```

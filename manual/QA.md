### **Question and Answer** 
***

#### how use assets Refrece count  
***
1. set DefaultSettings.enableAutoCollect = true
2. then use load method end with R return RefrenceData
3. when use asset, need invoke RefrenceData.Ref()
4. when unuse asset, need invoke RefrenceData.UnRef()
5. then asset data will auto manager self
6. tips:  
AssetBundle/SpriteAtlas will auto increase refrence count when you call sub asset Ref()

#### how to CI
***
Invoke build method in your Build Pipleline
``` csharp
// for package ios assetbundle
BuildHelper.BuildAssetBundle(BuildTarget.iOS, "Assets/[Editor]/**/{your asset project name}.asset");
// for build ios hotfix file
BuildHelper.CreateVersionFiles(RuntimePlatform.IPhonePlayer, "", "Assets/[Editor]/**/{your version asset name}.asset");
```

#### how to use self decrypt
***
1. enable encrypt in asset project, then you can use default encrypt 
 ![Enable encrypt](../Images/enable_encrypt.jpg)
2. set FileProcessor.customABEncrypt to your own encrypt method **before build asset project**
3. then set ResourceManager.Instance.abDecryptHandler to your own decrypt method **before resource manger initial**

#### how to support unity unsupport extension to assetbundle like lua
*** 
just add **bytes** extension
 ![Enable encrypt](../Images/custom_extension.jpg)

#### how preload assets
```csharp
await ResourceManager.Instance.PreloadAsync(
    new Dictionary<string, EResourceType>()
    {
        {"assetbundles/msic.ab", EResourceType.AssetBundle},
        {"assetbundles/common.ab", EResourceType.AssetBundle},
        {"assetbundles/ui.ab", EResourceType.AssetBundle},
    },
    p => { progress?.Invoke(p);
});
```
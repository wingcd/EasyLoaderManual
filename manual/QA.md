### **Question and Answer** 
***

#### can not find assets
***
1. check request paramaters, when you not use unique name mode, you need request with group/package name or you not has extension;   
   Anyway just request with suggestion;
2. maybe you need create mapper again;
3. when USE_BUNDLE mode, maybe you need build asset bundle again;
4. when USE_BUNDLE mode, check if unity asset bundle support the extension; 

#### same name when use unique name
1. add extension for name
2. add prefix/suffix for package files
3. set alias for files
4. rename files

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
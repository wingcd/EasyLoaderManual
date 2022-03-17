### **Asset Manager Window**

#### How To Open
***
* in menu bar Tools/EasyLoader/AssetManager
* use Alt+M
* double click asset project

#### Toolbar
***
* Current Asset Project (Keep last opened project)
* Create Mapper:  
create asset mapper file, will auto update when checked Auto Updater Mapper in AssetManger
* Build Asset Bundles:  
build asset bundles to Assign Folder(Default is StreamingAssets)
* Copy To  
copy all file in generate folder to Assign Folder, for save older version

#### Asset Project Settings  
***
* Auto Update Mapper  
will create/update mapper.json when files create/delete in UnityEditor
* Build Check  
validate asset bundle after generated(check missing files or create failed)
* Main AB Name  
main assetbundle name, just use defuault name is ok
* Target  
assetbundle build target platform
* AB Extension  
assetbundle extension name, default is ok
* Build Options
build pipline's build option
* Enable Encrypt  
if enabled, will encrypt assetbundle with a simple method, you can use your own encrypt algorithm(in FileProcessor.GetDefaultABEncyptFunction return your own encrypt method, then set ResourceManager.abDecryptHandler to you own decrypt method);
* Out Path  
where assetbunlde to generate, default is ok

#### **Package Sets**
#### 1. Toolbar
***
* show folder  
show folder in asset tree
* refresh  
refresh asset tree when filed change
* add  
add a empty packageset in this project(drag resource folder to window can be ok)
* delete  
delete all selected package sets

#### 2. Package Set Settings  
***
* Name  
when not a virtual package set, name just like a alias; but for virtual package set, name will for assetbundle file.
* Is Virtual  
virtual package set is a package, will build as a assetbundle.
* Asset Path  
when if not virtual, this property dirct to asset folder.
* File Mode  
> * Self  
package self(folders/files) to assetbundle
> * SubFiles  
package sub files to assetbundle
> * SubDirectories  
package sub directories to assetbundle
* Search Option
define how to search files

#### 3. Package Settings
***
* Name  
will be assetbudle file's name
* Ignore
if true, will ignore this package
* Need Package  
if true, this package will build to a assetbundle file when this folder is not under Resources folder. when you set copy dir, before build package will copy all file to this folder, then build the folder to assetbundle, so you can add a unity supported extension.
if false, you can set copy dir, then will copy files to all file to the folder under out path.
* Use Unique Name  
default is True, if true then you can load asset without path, only use file name can load asset in this package.
* With Extension  
if true, you need use filename with extension to load asset, and template must not be with extension.
if false, you need use filename without extension to load asset, and template may be need extension.
* Prefix  
if not empty, request filename will be add prefix on filename.
* Suffix  
if not empty, request filename will be add sufffix on filename.
* Template  
just for find file in package, filename will replace {0}
* Copy Dir  
see in Need Package
* Includes  
white regular list for find files
* Excepts  
black regular list for find files

#### 4. File Settings  
***
* Name  
default is file's name, you can change by yourself.
* Load Paramaters  
> * Method 1:  
    Group + Filename
> * Method 2:  (Enable Unique Name)  
    Filename

#### How To Use
***
* Create mapper file when you had add/delete files
* Initial Resource Manager by:
``` csharp
// use async mode need add ASYNC_SUPPROT define
await ResourceManager.Instance.InitialAsync();
// or 
await RM.InitialAsync();
```
* Then you can load asset which in mangered
``` csharp
// load prefab
var prefab = await RM.LoadAssetAsync<GameObject>("test.prefab");
// load sprite
var sprite1 = await RM.LoadAssetAsync<Sprite>("test.png");
// load sprite in atlas
var sprite2 = await RM.LoadSpriteFromAtlasAsync<GameObject>("icons.spriteatlas" "test.png");
// load scene
await RM.LoadSceneAsync("test.unity");
// load textasset
var text = await RM.LoadAssetAsync<TextAsset>("test.txt");
// load bytes
var bytes = await RM.LoadAssetAsync("test.bytes", byte[]);
```

#### Support Types
***
* Bytes
* Text
* AssetBundle
* AudioClip
* Texture2D
* Unity Asset Types ...

#### Naming Rules
***
##### Callback Mode: end with nothing
Like:
* Initial
* LoadAsset
* LoadAssetBundle
* LoadScene
* LoadSpriteFromAtlas
* ABPreload
* Preload

##### Async Mode: end with Async
Must add ASYNC_SUPPORT define

Like:
* InitialAsync
* LoadAssetAsync
* LoadAssetBundleAsync
* LoadSceneAsync
* LoadSpriteFromAtlasAsync
* ABPreloadAsync
* PreloadAsync

##### Sync Mode: end with Sync
Need preload assets before use

Like:
* InitialSync
* LoadAssetSync
* LoadAssetBundleSync
* LoadSceneSync
* LoadSpriteFromAtlasSync
* ABPreloadSync
* PreloadSync

##### Specail End Tag
* With R, means return RefrenceObject
* With F, means use fullpath to load data
* With G, means load asset with group name
  
Like:
* LoadAssetR
* LoadAssetF
* LoadAssetG
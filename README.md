# ShalltyUtils
A utility plugin focused on enhancing Timeline to improve animator's workflows by incorporating handy extra features.

### HOW TO INSTALL:
1. Download and install all the **Requirements**.
   
- [BepInEx 5](https://github.com/BepInEx/BepInEx)
- [IllusionModdingAPI](https://github.com/IllusionMods/IllusionModdingAPI)
- [HSPlugins](https://github.com/IllusionMods/HSPlugins)

  
2. Download the lastest ShalltyUtils according to your game;
   
| `KK`           | `KKS`          |      `HS2`  |
|:---------------|:----------------| :----------|
| Koikatsu       | Koikatsu Sunshine | HoneySelect2|
| Koikatsu Party |


3. Extract the **.DLL** file inside the `BepInEx\plugins` folder in your game directory.

### DOCUMENTATION:
Documentation for all plugin versions can be found in this [MEGA folder](https://mega.nz/folder/pG5zVAQb#dSeETBR2R-Q89U4ftAAiKQ)

### BUILD / RELEASE NOTES (fork maintainers):
This repo cannot be built from source on this machine: the KK project imports `..\..\Shared`, `..\..\ToolBox` and `..\..\packages`, which are not part of the repository. Instead, the KK release DLL is produced by **patching the previous release DLL (IL level) with Mono.Cecil**:

1. Start from `bin\KK_ShalltyUtils.dll` (the last released build; also what is installed in `H:\Koikatsu\BepInEx\plugins`).
2. Load it with `Mono.Cecil.dll` (copy it from `H:\Koikatsu\BepInEx\core`) in PowerShell, using a resolver with `BepInEx\core`, `BepInEx\plugins` and `CharaStudio_Data\Managed` as search directories.
3. Apply the same change that was made in the C# source to the matching method (for lambdas look inside the `<>c__DisplayClassXX_0` type; reference `UnityEngine.dll` from `CharaStudio_Data\Managed` for Unity calls), then write the assembly.
4. Copy the result over `bin\KK_ShalltyUtils.dll` and `H:\Koikatsu\BepInEx\plugins\KK_ShalltyUtils.dll`.
5. Release: `Compress-Archive -Path bin\KK_ShalltyUtils.dll -DestinationPath bin\KK_ShalltyUtils.zip -Force`, then `gh release create vX.Y.Z-KK bin/KK_ShalltyUtils.zip --repo vaz1306011/ShalltyUtils --target master`.

Keep the C# source and the patched DLL in sync: every source change that is shipped must also be patched into the DLL. Only the KK build is produced this way (KKS and HS2 are not included).

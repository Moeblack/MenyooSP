<img width="1280" height="720" alt="Menyoo banner" src="https://github.com/user-attachments/assets/6ce3c340-a0a3-4f47-90a7-37e1f4d674f3" />

# Menyoo 2.0 简体中文分支

基于 [itsjustcurtis/MenyooSP](https://github.com/itsjustcurtis/MenyooSP) 的**原生外置简体中文资源**及**菜单字体默认设置**，保留上游全部功能。

> 本仓库是上游的非官方简体中文分支（fork），**不是**官方中文版

## 本分支的中文改动

- 新增外置词典 `ChineseSimplified.json`，放在上游真正的随包语言资源目录 `menyooStuff/Language/` 下，由 Menyoo 原生的外置语言机制加载（不修改 `Menyoo.asi`）。
- 对主菜单及常用功能做了补译与术语修正。例如 Triggerbot 译为“自动扳机”——它需要先瞄中目标后才开火，并非全自动搜敌/锁头。
- 发布模板默认选择简体中文：`[settings] language = ChineseSimplified`。
- 发布模板默认把四项菜单字体设为 `0`：`[fonts] title / options / selection / breaks = 0`。这是让中文正常显示的必要字体配置（`0` = 游戏内置常规字体，会随游戏语言加载中文字形；上游默认的 7/4/4/1 是 Pricedown/Impact/Italic 等显示字体，通常不含中文字形）。

## 已经装好 Menyoo 2.0 的用户

1. 从本仓库获取词典文件：[`Solution/source/_Build/bin/Release/menyooStuff/Language/ChineseSimplified.json`](Solution/source/_Build/bin/Release/menyooStuff/Language/ChineseSimplified.json)
2. 放到你游戏根目录下的 `menyooStuff/Language/ChineseSimplified.json`。
3. **先完全退出游戏**，再只修改你现有的 `menyooStuff/menyooConfig.ini` 中下面五项（其余设置保持你原来的，避免覆盖个人设置）：

   ```ini
   [settings]
   language = ChineseSimplified

   [fonts]
   title = 0
   options = 0
   selection = 0
   breaks = 0
   ```

4. 重新启动游戏。

> 注意：Menyoo 在运行时大约每 30 秒会把内存中的设置写回 `menyooConfig.ini`。因此**不要开着游戏从外部改这个 ini**，否则你的改动会被内存中的旧值覆盖。请完全退出游戏后再改。

## 全新安装

1. 先安装上游稳定版 Menyoo（本仓库是源码/中文资源分支，仓库的源码 ZIP **不能**当作可直接运行的预编译插件）：

   - 上游 Releases：<https://github.com/itsjustcurtis/MenyooSP/releases>
   - 或 GTA5-Mods 页面：<https://www.gta5-mods.com/scripts/menyoo-2-0>

2. 按上游说明把 `Menyoo.asi` 与 `menyooStuff` 文件夹放入 GTA V 根目录（与 `GTA5.exe` 同级）。
3. 再按上一节放入中文词典，并设置那五项默认值。

## 运行依赖（以作者发布页为准）

**增强版（GTA V Enhanced）：**

- 最新版 ScriptHookV：<http://www.dev-c.com/gtav/scripthookv/>
- OpenRPF 提供的 Enhanced ASI Loader：<https://www.gta5-mods.com/tools/openrpf-openiv-asi-for-gta-v-enhanced>
- Windows 11 需要 alloc8or 的 DirectStorageFix：<https://www.gta5-mods.com/scripts/directstoragefix>
- 在 Rockstar 启动器设置里关闭 BattlEye（仅单机）

**旧版（Legacy）：**

- 使用 OpenIV 内置的 ASI Loader：<https://openiv.com/>
- 注意：Legacy 与 Enhanced 的 ASI Loader 不同。**不要**把 Legacy 的加载器（例如 `dinput8.dll`）一律套用到增强版；增强版请使用上面 OpenRPF 的方案。

## 使用

- 按 **F8** 打开/关闭菜单。
- 切换语言：**设置 → 语言 → 简体中文**；菜单里也提供“重新加载语言文件”。
- 如果菜单显示为方框，字体更改请以“**完全退出游戏 → 把 `menyooConfig.ini` 的 `[fonts]` 四项改为 0 → 重新启动游戏**”为准，不要在方框菜单里盲按。

## 范围与限制

- 中文能否显示依赖游戏是否加载了中文字形，**请把游戏语言设置为简体中文**。
- 部分动态拼接字符串、内部模型/资源代码，以及游戏自身的名称，不受外置词典完整控制（会回退显示原文）。
- 本分支未在游戏内做验证，不保证“所有方框都已解决”或“全版本兼容”。

## 从源码构建（说明，未在本分支运行构建）

- 需要 Visual Studio 2022（含 **Desktop development with C++** 工作负载）与 Windows 10/11 SDK。
- 仓库使用 git 子模块（`pugixml`、`simpleini`、`dirent`、`MinHook`），需递归克隆：

  ```sh
  git clone --recurse-submodules https://github.com/Moeblack/MenyooSP.git
  # 若已非递归克隆：
  git submodule update --init --recursive
  ```

- 用 Premake5 生成解决方案：

  ```sh
  generate.bat
  ```

- 在 Visual Studio 2022 中打开 `Solution/Menyoo.sln` 并构建 `Release | x64`，或在 Developer Command Prompt 中：

  ```sh
  msbuild /m /p:Configuration=Release /p:Platform=x64 Solution\Menyoo.sln
  ```

- 产物：`Solution/source/_Build/bin/Release/Menyoo.asi`（运行时需要 Microsoft Visual C++ Redistributable x64）。

## 致谢与许可

- 上游项目：[MAFINS/MenyooSP](https://github.com/MAFINS/MenyooSP)（原作者 MAFINS）与 [itsjustcurtis/MenyooSP](https://github.com/itsjustcurtis/MenyooSP)（ItsJustCurtis 及贡献者）。
- 简体中文词典基底：[lucienlmy/Menyoo-Translation](https://github.com/lucienlmy/Menyoo-Translation)；本分支在其基础上对当前版本菜单做了补译与术语修订。
- 本项目遵循上游的 [GNU GPL v3](LICENSE.txt) 许可。源码中来自其他项目的部分在其出现处标注各自的许可。
- 上游社区：Discord <https://discord.gg/v29AwqAemT> ｜ Patreon <https://www.patreon.com/c/ItsJustCurtis>

# 第二十二天: C++ 額外認識-二

延續昨天訂的目標，今天就先來看 C++的`Logging` library~

那要用哪個 C++的 logging library 這個問題，就交給 Google 大神囉，嘿嘿

所以就有了答案，我們要來使用 `spdlog`

## spdlog

從[spdlog](https://github.com/gabime/spdlog)的 github 簡介可以看到:

> About: Fast C++ logging library.

那通常看到一個這樣的第三方套件，在 C#或 Python，馬上就會想到可以使用套件管理器(C# - nuget, python - pip)來安裝，那 C++的呢?

這邊就先來介紹 Microsoft 推出的 C++ 套件管理器 `vcpkg`

## vcpkg

[vcpkg](https://github.com/microsoft/vcpkg) 是微軟推出讓 C++的使用者可以使用的套件管理器

這邊就照著官方的教學來安裝與使用吧

### Windows Install

Prerequisites:

- [Git](https://git-scm.com/downloads)
- Windows 7 or newer
- [Visual Studio](https://visualstudio.microsoft.com/zh-hant/) 2015 Update 3 or greater with the English language pack

1. 下載 vcpkg 並安裝，官方有建議的路徑`C:\src\vcpkg` 或 `C:\dev\vcpkg`，就看個人的喜好囉

```
> git clone https://github.com/microsoft/vcpkg
> .\vcpkg\bootstrap-vcpkg.bat
```

安裝完可以執行`vcpkg version`來確認安裝有沒有成功

```
E:\>vcpkg version
vcpkg package management program version 2022-09-20-522aa94e9d261c7d7b2f079bf2591ca62df5c714

See LICENSE.txt for license information.
```

2. (可選)，將vcpkg的檔案路徑加到環境變數

[env]

[env2]

[env3]

[env4]

3. 如果要在`Visual Studio`裡面也能使用的話，我們還要執行下面的指令，成功就會看到下面的訊息

```
> vcpkg integrate install
Applied user-wide integration for this vcpkg root.
CMake projects should use: "-DCMAKE_TOOLCHAIN_FILE=E:/vcpkg/scripts/buildsystems/vcpkg.cmake"

All MSBuild C++ projects can now #include any installed libraries. Linking will be handled automatically. Installing new libraries will make them instantly available.
```

## spdlog install

安裝完`vcpkg`後，就可以透過`vcpkg`來下載`spdlog`囉


`note: vcpkg 在 Windows 中預設是x86版本，如果要安裝x64，需要補上 :x64-windows`

```
> vcpkg install spdlog:x64-windows
```

安裝好了之後，再度打開`Visual Studio 2022`，一樣是新建一個C++ ConsoleApp當範例，這時候可以看到使用`#include <spdlog/spdlog.h>`，VS會幫我們去抓安裝在本機上的套件

[console_app]

[console_result]

---

好囉，那明天就接著來看看其他有關C++的額外認識囉~

## 參考資料

[spdlog - github](https://github.com/gabime/spdlog)

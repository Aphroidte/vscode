# 1. C/C++ for Visual Studio Code

Table of Contents

- [1. C/C++ for Visual Studio Code](#1-cc-for-visual-studio-code)
  - [1.1. 先决条件](#11-先决条件)
  - [1.2. C/C++ 扩展概述](#12-cc-扩展概述)
  - [1.3. C/C++ 扩展的特性](#13-cc-扩展的特性)
  - [1.4. 自定义默认设置](#14-自定义默认设置)
    - [1.4.1. 更新了 `c_cpp_properties.json` 语法](#141-更新了-c_cpp_propertiesjson-语法)
    - [1.4.2. 系统  include path/defines 解析策略](#142-系统--include-pathdefines-解析策略)
  - [1.5. Quick links](#15-quick-links)
  - [1.6. Questions and feedback](#16-questions-and-feedback)
  - [1.7. 参考链接](#17-参考链接)

## 1.1. 先决条件

C/C++ 扩展 **不包括 C++ 编译器或调试器**。您将需要安装这些工具或使用您计算机上已安装的工具。

- 安装 **C++ 编译器**
- 安装 **C++ 调试器**

以下是该扩展正式支持的每个平台的编译器和架构列表。请注意，对其他编译器的支持可能会受到限制。

| Platform | 编译器           | 架构                 |
| :------- | :--------------- | :------------------- |
| Windows  | MSVC, Clang, GCC | x64, x86, arm64, arm |
| Linux    | Clang, GCC       | x64, x86, arm64, arm |
| macOS    | Clang, GCC       | x64, x86, arm64      |

有关安装所需工具或设置扩展的更多信息，请按照以下教程进行操作。

## 1.2. C/C++ 扩展概述

*Visual Studio Code* 的 *C/C++* 支持由 *Microsoft C/C++ 扩展* 提供，以在 *Windows*、*Linux* 和 *macOS* 上实现跨平台 *C* 和 *C++* 开发。

安装扩展后，当您打开或创建 `*.cpp` 文件时，您将拥有语法高亮（着色）、智能完成和悬停（智能感知）以及错误检查。

介绍视频：[Introductory Videos](https://code.visualstudio.com/docs/cpp/introvideos-cpp)

每个编译器和平台的 C/C++ 扩展教程:

- [Microsoft C++ compiler (MSVC) on Windows](https://code.visualstudio.com/docs/cpp/config-msvc)
- [GCC and Mingw-w64 on Windows](https://code.visualstudio.com/docs/cpp/config-mingw)
- [GCC on Windows Subsystem for Linux (WSL)](https://code.visualstudio.com/docs/cpp/config-wsl)
- [GCC on Linux](https://code.visualstudio.com/docs/cpp/config-linux)
- [Clang on macOS](https://code.visualstudio.com/docs/cpp/config-clang-mac)
- [CMake Tools on Linux](https://code.visualstudio.com/docs/cpp/cmake-linux)

## 1.3. C/C++ 扩展的特性

详情请参阅：[Edit C++ in Visual Studio Code](https://code.visualstudio.com/docs/cpp/cpp-ide)

在这里重点介绍一些用法:

1. 在源文件中搜索成员：`Ctrl+P` 并输入 `@`/`#` 字符，即可列出并搜索该文件/当前工作区的一些符号/成员。也可以直接使用快捷键 `Ctrl + Shift + O` 进行搜索. 效果是一样的. 要在整个工作区搜索符号, 请使用 `Ctrl + T`
2. 代码格式化: 使用格式化文档 (`Shift+Alt+F`) 格式化整个文件，或者使用右键单击上下文菜单中的格式化选择 (`Ctrl+K Ctrl+F`) 仅格式化当前选择. 您还可以使用以下设置配置自动格式化：`editor.formatOnSave` (保存文件时进行格式化), `editor.formatOnType`(在您键入时进行格式化（在 ; 字符上触发）)
3. 查看符号的定义: 将光标放在源代码中使用符号的任何位置，然后按 `Alt+F12`。或者，您可以从上下文菜单中选择 `Peek Definition`（右键单击，然后选择 `Peek Definition`）。

## 1.4. 自定义默认设置

以下 C_Cpp.default.* 设置映射到 c_cpp_properties.json 配置块中的每个属性。即：

```json
C_Cpp.default.includePath                          : string[]
C_Cpp.default.defines                              : string[]
C_Cpp.default.compileCommands                      : string
C_Cpp.default.macFrameworkPath                     : string[]
C_Cpp.default.forcedInclude                        : string[]
C_Cpp.default.intelliSenseMode                     : string
C_Cpp.default.compilerPath                         : string
C_Cpp.default.cStandard                            : c89 | c99 | c11 | c17
C_Cpp.default.cppStandard                          : c++98 | c++03 | c++11 | c++14 | c++17 | c++20
C_Cpp.default.browse.path                          : string[]
C_Cpp.default.browse.databaseFilename              : string
C_Cpp.default.browse.limitSymbolsToIncludedHeaders : boolean
```

您可以在“用户”设置中为 `C_Cpp.default.cppStandard` 设置一个全局值，并将其应用于您打开的所有文件夹。 如果任何一个文件夹需要不同的值，您可以通过添加“文件夹”或“工作区”值来覆盖该值。*VS Code* 设置的此属性允许您独立配置每个工作区 - 使 `c_cpp_properties.json` 文件可选。

### 1.4.1. 更新了 `c_cpp_properties.json` 语法

在 `c_cpp_properties.json` 的可接受语法中添加了一个特殊变量，该变量将指示扩展从上述 *VS* 代码设置中插入值。 如果您将 `c_cpp_properties.json` 中任何设置的值设置为 `${default}`，它将指示扩展程序读取该属性的 `VS Code` 默认设置并插入它。 例如：

```json
"configurations": [
    {
        "name": "Win32",
        "includePath": [
            "additional/paths",
            "${default}"
        ],
        "defines": [
            "${default}"
        ],
        "macFrameworkPath": [
            "${default}",
            "additional/paths"
        ],
        "forcedInclude": [
            "${default}",
            "additional/paths"
        ],
        "compileCommands": "${default}",
        "browse": {
            "limitSymbolsToIncludedHeaders": true,
            "databaseFilename": "${default}",
            "path": [
                "${default}",
                "additional/paths"
            ]
        },
        "intelliSenseMode": "${default}",
        "cStandard": "${default}",
        "cppStandard": "${default}",
        "compilerPath": "${default}"
    }
],
```

请注意，对于接受 `string[]` 的属性，上面建议的语法允许您使用附加值扩充 `VS Code` 设置，从而允许您在 `VS Code` 设置和 `c_cpp_properties.json` 中的配置特定设置中列出公共路径。

有关 `c_cpp_properties.json` 设置文件的详细信息，请参阅 [c_cpp_properties.json reference](https://code.visualstudio.com/docs/cpp/c-cpp-properties-schema-reference)

### 1.4.2. 系统  include path/defines 解析策略

请参阅: [Customizing default settings](https://code.visualstudio.com/docs/cpp/customize-default-settings-cpp)

## 1.5. Quick links

- [增强的着色 (Enhanced colorization)](https://code.visualstudio.com/docs/cpp/colorization-cpp)
- [C/C++ 扩展日志记录](https://code.visualstudio.com/docs/cpp/enable-logging-cpp)
- [Debug C++ in Visual Studio Code](https://code.visualstudio.com/docs/cpp/cpp-debug)
- [Configure C/C++ debugging](https://code.visualstudio.com/docs/cpp/launch-json-reference)

## 1.6. Questions and feedback

- [FAQs](https://code.visualstudio.com/docs/cpp/faq-cpp)
- [Provide feedback](https://github.com/microsoft/vscode-cpptools/issues/new/choose)
- [Known issues](https://github.com/Microsoft/vscode-cpptools/issues)
- [Quick survey](https://www.research.net/r/VBVV6C6)

## 1.7. 参考链接

- [1] [C/C++ extension overview](https://code.visualstudio.com/docs/languages/cpp) [j].code.visualstudio.com

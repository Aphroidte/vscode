# 1. Go for Visual Studio Code

Table of Contents

- [1. Go for Visual Studio Code](#1-go-for-visual-studio-code)
  - [1.1. 简介](#11-简介)
  - [1.2. Quick Start](#12-quick-start)
  - [1.3. 功能亮点](#13-功能亮点)
  - [1.4. Tools](#14-tools)
  - [1.5. 设置您的工作区](#15-设置您的工作区)
  - [1.6. 个性化配置](#16-个性化配置)
  - [1.7. 故障排除](#17-故障排除)

## 1.1. 简介

现在可以通过 *Delve v1.7.3* 或更高版本的 *Delve* 原生 *DAP* 实现进行 [远程连接调试](https://github.com/golang/vscode-go/wiki/debugging#connecting-to-headless-delve-with-target-specified-at-server-start-up)。它使用已用于本地调试的相同 [调试功能](https://github.com/golang/vscode-go/wiki/debugging) 增强了远程调试。它现在是扩展的 [Go Nightly](https://github.com/golang/vscode-go/wiki/nightly) 构建的默认设置，并将在 2022 年中期成为稳定版本的默认设置。我们建议现在在 `launch.json` 中切换远程附加配置以使用 `"debugAdapter":"dlv-dap"`。如果遇到任何问题，请 [提交新问题](https://github.com/golang/vscode-go/issues/new/choose)。

观看 [GopherCon 2021](https://www.gophercon.com/) 的 [调试寻宝游戏](https://youtu.be/ZPIPPRjwg7Q)，以有趣的方式使用 *VS Code Go* 和 *Delve DAP* 进行调试演示。

## 1.2. Quick Start

1. 如果您还没有安装 [Go](https://golang.org/) 1.14 或更新版本。
2. 安装 [VS Code Go 扩展](https://marketplace.visualstudio.com/items?itemName=golang.go)。
3. 打开包含 Go 代码的任何目录或工作区以自动激活扩展。 [Go 状态栏](https://github.com/golang/vscode-go/wiki/ui) 出现在窗口的左下角，并显示您的 Go 版本。
4. 扩展依赖于 `go、gopls、dlv` 和其他可选工具。如果缺少任何依赖项，则会显示 `⚠️ 缺少分析工具` 警告。单击警告以下载依赖项。

有关扩展所依赖的 [工具的完整列表](https://github.com/golang/vscode-go/wiki/tools)，请参阅工具文档。

## 1.3. 功能亮点

有关更多详细信息，请参阅 [完整的功能细分](https://github.com/golang/vscode-go/wiki/features)。

除了集成的编辑功能外，该扩展还提供了几个用于处理 Go 文件的命令。有关更多详细信息，请参阅 [此扩展提供的命令的完整列表](https://github.com/golang/vscode-go/wiki/commands#detailed-list)。

> ⚠️ Note: *Go* 文件的默认语法突出显示由嵌入在 *VS Code* 中的 *TextMate* 规则提供，而不是由此扩展提供。

为了更好地突出显示语法，我们建议通过打开 *Gopls* 的 `ui.semanticTokens` 设置来启用语义突出显示。 `“gopls”：{“ui.semanticTokens”：true}`

## 1.4. Tools

该扩展使用了一些由 *Go* 社区开发的命令行工具。特别是，必须安装 `go`、`gopls` 和 `dlv` 才能使此扩展正常工作。有关扩展所依赖的工具的完整列表，请参阅 [工具文档](https://github.com/golang/vscode-go/wiki/tools)。

为了找到这些命令行工具，扩展程序会搜索 `GOPATH/bin` 以及在 `PATH` 环境变量（或 Windows 上的 Path）中指定的目录，*VS Code* 进程已从这些目录中启动。如果找不到工具，扩展程序会提示您安装缺少的工具，并在右下角显示 `“⚠️缺少分析工具”` 警告。请通过响应警告通知或手动运行 `Go: Install/Update Tools` 命令来安装它们。

## 1.5. 设置您的工作区

*Go* 模块是 *Go* 在最新版本的 *Go* 中管理依赖项的方式。模块取代了基于 *GOPATH* 的方法来指定在给定构建中使用哪些源文件，它们是 `go1.16+` 中的默认构建模式。虽然此扩展继续支持 *Go* 模块和 *GOPATH* 模式，但我们强烈建议在模块模式下进行 *Go* 开发。如果您正在处理现有项目，请考虑迁移到模块。

与传统的 *GOPATH* 模式不同，模块模式不需要工作空间位于 *GOPATH* 下，也不需要使用特定的结构。模块由 *Go* 源文件的目录树定义，在树的根目录中有一个 `go.mod` 文件。

您的项目可能涉及一个或多个模块。如果您使用多个模块或不常见的项目布局，您将需要使用 [工作区文件夹](https://code.visualstudio.com/docs/editor/multi-root-workspaces) 来配置您的工作区。请参阅 [有关支持的工作区布局的文档](https://github.com/golang/tools/blob/master/gopls/doc/workspace.md)。

## 1.6. 个性化配置

扩展不需要配置，应该可以开箱即用。但是，您可能希望调整设置以自定义其行为。请参阅 [设置文档](https://github.com/golang/vscode-go/wiki/settings) 以获取完整的设置列表。有关进一步的自定义和独特的用例，请参阅 [高级主题](https://github.com/golang/vscode-go/wiki/advanced)。

## 1.7. 故障排除

如果扩展程序未按预期工作，您可以查看我们的 [故障排除指南](https://github.com/golang/vscode-go/wiki/troubleshooting)。有一个用于一般故障排除，另一个专门用于 [对调试功能进行故障排除](https://github.com/golang/vscode-go/wiki/debugging#troubleshooting)。

# 1. Makefile Tools

Table of Contents

- [1. Makefile Tools](#1-makefile-tools)
  - [1.1. 激活扩展](#11-激活扩展)
  - [1.2. 预配置您的项目](#12-预配置您的项目)
  - [1.3. 配置您的项目](#13-配置您的项目)
  - [1.4. 建筑目标](#14-建筑目标)
  - [1.5. 调试和运行目标](#15-调试和运行目标)
  - [1.6. 故障排除](#16-故障排除)
  - [1.7. 参考链接](#17-参考链接)

## 1.1. 激活扩展

当它在 `${workspaceFolder}` 中找到 *Makefile* 时，扩展将激活。如果您的 *Makefile* 不在文件夹的根目录中，请使用 `makefile.makefilePath`（生成 **make 开关 -f**）或 `makefile.makeDirectory`（生成 **make 开关 -C**）设置来指示扩展在哪里找到它。

## 1.2. 预配置您的项目

如果您需要在配置/构建之前设置任何环境变量或运行任何终端操作（如通常的 `./autogen.sh`、`./configure` 或 `vcvarsall.bat`），则需要从已经存在的终端启动 *VSCode* 根据您的项目要求进行设置，或者您可以将 `makefile.preConfigureSript` 设置指向一个批处理脚本文件，并通过命令面板板中的命令 `makefile.preconfigure` 随时调用它。 通过将 `makefile.alwaysPreConfigure` 设置为 *true*，您无需单独运行预配置命令。扩展将在每次配置操作之前调用脚本。

## 1.3. 配置您的项目

默认情况下，扩展将尝试使用位于 `$PATH` 中的 *make* 程序来配置项目。如果您使用不同风格的 *make* 工具，或者它不在您的 `$PATH` 中，请使用 `makefile.makePath` 设置来指示扩展在哪里找到它。提供系统路径中的文件/命令，前缀为 `${workspaceRoot}`，或绝对路径，因为无法正确解析相对路径。

如果您将 `makefile.buildLog` 设置指向构建的输出，则扩展还可以避免在配置项目时运行 *make* 程序。

**授予 Makefile Tools 配置 IntelliSense 的权限**：通过运行 `C/C++: Change Configuration Provider...` 命令并从列表中选择 *Makefile Tools* 来授予 *Makefile Tools* 配置 *IntelliSense* 的权限。

> **注意**：如果您需要将其他参数传递给 *make*，则应使用 `makefile.configurations` 设置创建配置对象并使用 *makeArgs* 属性指定要传递给 make 的参数。您还可以在此对象中配置其他选项。如果您以多种不同的方式配置 make，您可以使用不同的参数创建多个配置对象。只需确保为您的配置提供一个唯一的名称，以便您可以将它们区分开来。

## 1.4. 建筑目标

要构建目标，请运行 `Makefile: Set the make launch configuration` 命令设置要构建的目标（默认目标为“all”），然后运行 `Makefile: Build the current target`。还有一些方便的命令可以构建 *ALL*、构建 *clean* 等，而无需更改您的活动构建目标。

## 1.5. 调试和运行目标

要调试或运行目标，请运行 `Makefile: Set the make launch configuration` 命令并选择要调试或运行的目标。如果该目标的配置尚未添加到 `makefile.launchConfigurations` 设置中，那么此时将为您添加一个。然后运行 `Makefile: Debug the selected binary target` 或 `Makefile: Run the selected binary target in the terminal` 以开始调试或在没有附加调试器的情况下运行目标。

如果您需要向目标传递其他参数，请通过将 *binaryArgs* 属性添加到配置来更新 `makefile.launchConfigurations`。

## 1.6. 故障排除

我们记录了我们测试过的选定数量的存储库所需的设置和配置。可以在此处找到该文档：[docs/repositories.md](https://github.com/Microsoft/vscode-makefile-tools/blob/master/docs/repositories.md)。欢迎对本文档的贡献（例如，对于我们尚未测试的其他存储库）。

可以在此处找到更深入的故障排除指南：[docs/troubleshooting.md](https://github.com/Microsoft/vscode-makefile-tools/blob/master/docs/troubleshooting.md)

## 1.7. 参考链接

- [1] [Makefile Tools](https://marketplace.visualstudio.com/items?itemName=ms-vscode.makefile-tools) [j].marketplace.visualstudio.com

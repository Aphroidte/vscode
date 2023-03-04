# 1. `markdownlint`

- [1. `markdownlint`](#1-markdownlint)
  - [1.1. 官方文档](#11-官方文档)
    - [1.1.1. Introduction](#111-introduction)
    - [1.1.2. Usage](#112-usage)
    - [1.1.3. Rules](#113-rules)
    - [1.1.4. 命令](#114-命令)
      - [1.1.4.1. 修复命令](#1141-修复命令)
      - [1.1.4.2. Workspace](#1142-workspace)
      - [1.1.4.3. 禁用](#1143-禁用)
    - [1.1.5. 配置](#115-配置)
      - [1.1.5.1. markdownlint.config](#1151-markdownlintconfig)
      - [1.1.5.2. markdownlint.focusMode](#1152-markdownlintfocusmode)
      - [1.1.5.3. markdownlint.run](#1153-markdownlintrun)
      - [1.1.5.4. markdownlint.ignore](#1154-markdownlintignore)
      - [1.1.5.5. markdownlint.customRules](#1155-markdownlintcustomrules)
      - [1.1.5.6. markdownlint.lintWorkspaceGlobs](#1156-markdownlintlintworkspaceglobs)
    - [1.1.6. 抑制告警](#116-抑制告警)
    - [1.1.7. Snippets](#117-snippets)
    - [1.1.8. 安全](#118-安全)

## 1.1. 官方文档

> 详见 markdownlint [官方文档](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)

markdownlint 是一个 Visual Studio Code 的扩展插件；用于对 Markdown/CommonMark 的样式或语法进行检查。

### 1.1.1. Introduction

[Markdown](https://en.wikipedia.org/wiki/Markdown) 标记语言旨在易于阅读、编写和理解。它的灵活性既是优点也是缺点。许多样式都是可能的，因此格式可能不一致。某些构造在所有解析器中都不能很好地工作，应该避免。例如，这里有 [一些常见/麻烦的 Markdown 结构。](https://gist.github.com/DavidAnson/006a6c2a2d9d7b21b025)

[markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint) 是 Visual Studio Code 编辑器的扩展，它包含一个规则库，以鼓励 Markdown 文件的标准和一致性。它由 Node.js 的 markdownlint 库提供支持（灵感来自 [Ruby 的 markdownlint](https://github.com/mivok/markdownlint)）。本扩展由 [markdownlint-cli2 引擎](https://github.com/DavidAnson/markdownlint-cli2) 执行，可与此扩展配合使用，为脚本和持续集成场景提供命令行支持。[markdownlint-cli2-action GitHub Action](https://github.com/marketplace/actions/markdownlint-cli2-action) 使用相同的引擎，并且可以与项目工作流集成。

### 1.1.2. Usage

在安装了 `markdownlint` 的代码中编辑 Markdown 文件时，任何违反 `markdownlint` 规则之一的行（见下文）都会在编辑器中触发警告。警告由绿色波浪下划线指示，也可以通过按 `Ctrl+Shift+M/⇧⌘M` 打开 “错误和警告” 对话框来查看。将鼠标指针悬停在绿线上查看警告或按 F8 和 `Shift+F8/⇧F8` 循环浏览所有警告（markdownlint 警告均以 `MD###` 开头）。

有关 `markdownlint` 警告的更多信息，请将光标放在一行上并单击灯泡图标或按 `Ctrl+./⌘`。打开快速修复对话框。单击对话框中的警告之一将在默认 Web 浏览器中显示该规则的帮助条目。

> 注：有关教程，请参阅 Dave Johnson 的 [《Build an Amazing Markdown Editor Using Visual Studio Code and Pandoc》](https://thisdavej.com/build-an-amazing-markdown-editor-using-visual-studio-code-and-pandoc/)

### 1.1.3. Rules

有关更多详细信息，请参阅 [markdownlint 的 Rules.md 文件](https://github.com/DavidAnson/markdownlint/blob/main/doc/Rules.md)

通过将光标移动到违反规则（波浪形下划线文本）并键入 `Ctrl+./⌘`，可以自动修复以下规则。或单击灯泡图标。

### 1.1.4. 命令

#### 1.1.4.1. 修复命令

所有违反上述规则的文档都可以自动修复。`markdownlint` 将自己注册为 Markdown 文件的 [源代码格式化程序](https://code.visualstudio.com/docs/editor/codebasics#_formatting)，并且可以通过 `Format Document/editor.action.formatDocument` 和 `Format Selection/editor.action.formatSelection` 命令调用。

- `Shift + Alt + F/⇧⌥F`：格式化文本。（与 Markdown All in One 插件冲突了）
- `Ctrl+K Ctrl+F/⌘K ⌘F`：格式化段落。

要在保存或粘贴到 Markdown 文档时自动格式化，请配置 Visual Studio Code 的 editor.formatOnSave 或 editor.formatOnPaste 设置，如下所示：

```json
"[markdown]": {
    "editor.formatOnSave": true,
    "editor.formatOnPaste": true
},
```

`markdownlint` 还提供了 `markdownlint.fixAll` 命令，该命令可以一步修复文档的违规行为，并且可以从命令面板，运行命令 `fix supported markdownlint violations in the document` 或 通过 [将命令绑定到键盘快捷键](https://code.visualstudio.com/docs/getstarted/keybindings) 来运行。

要在保存 Markdown 文档时自动修复违规，请配置 Visual Studio Code 的 `editor.codeActionsOnSave` 设置，如下所示：

```json
"editor.codeActionsOnSave": {
    "source.fixAll.markdownlint": true
}
```

通过编辑|撤消或 `Ctrl+Z/⌘Z` 可以恢复来自任一方法的自动应用修复。

#### 1.1.4.2. Workspace

要检查当前工作区中的所有 Markdown 文件，请运行 `markdownlint.lintWorkspace` 命令（从命令面板或通过将其绑定到键盘快捷键）。这将使用为扩展提供动力的同一引擎 [markdownlint-cli2](https://github.com/DavidAnson/markdownlint-cli2) 来检查所有文件并将结果输出到“终端”面板中的新终端。结果也将出现在“问题”面板中（`Ctrl+Shift+M/⇧⌘M`），因为扩展中包含问题匹配器。可以单击“问题”面板中的条目以在编辑器中打开相应的文件。要自定义 linting 工作区时包含/排除的文件，请配置 `markdownlint.lintWorkspaceGlobs` （见下文）

#### 1.1.4.3. 禁用

要暂时禁用 Markdown 文档的 linting，请运行 `markdownlint.toggleLinting` 命令。要重新启用 linting，请再次运行 `markdownlint.toggleLinting` 命令。

> 注：`markdownlint.toggleLinting` 命令的效果在打开新工作区时重置； linting 默认为启用

### 1.1.5. 配置

#### 1.1.5.1. markdownlint.config

默认规则配置禁用 MD013/line-length，因为许多文件包含的行长于传统的 80 个字符限制：

```json
{
    "MD013": false
}
```

> 注：`MD002/first-heading-h1` 和 `MD006/ul-start-left` 也被禁用，因为它们在 markdownlint 库中已被弃用。

可以在项目中的任何目录下，通过创建名为的 `.markdownlint.jsonc/.markdownlint.json` 的 [JSON](https://en.wikipedia.org/wiki/JSON) 文件 或名为 `.markdownlint.yaml/.markdownlint.yml` 的 [YAML](https://en.wikipedia.org/wiki/YAML) 文件 或名为 `.markdownlint.cjs` 的 [JavaScript](https://en.wikipedia.org/wiki/JavaScript) 文件来启用、禁用和自定义规则。

此外，可以通过创建名为 `.markdownlint-cli2.jsonc` 的 JSON 文件或名为 `.markdownlint-cli2.yaml` 的 YAML 文件或名为 `.markdownlint-cli2.cjs` 的 JavaScript 文件来配置选项（包括规则和诸如 [markdown-it 插件](https://www.npmjs.com/search?q=keywords:markdown-it-plugin) 和其他设置之类的东西）。

有关配置文件优先级和完整示例的更多信息，请参阅 [markdownlint-cli2 README.md 的配置部分](https://github.com/DavidAnson/markdownlint-cli2#configuration)。

> 注：当没有打开文件夹时，将从用户的主目录加载配置和选项（例如，Windows 上的 `%USERPROFILE%`或 macOS/Linux 上的 `$HOME`）。由于 JavaScript 代码在加载后会被缓存，因此对 `.markdownlint.cjs` 和 `.markdownlint-cli2.cjs` 的编辑需要重新启动 VS Code。

自定义配置通常由项目根目录中的 .markdownlint.json 文件定义：

```json
{
    "default": true,
    "MD003": { "style": "atx_closed" },
    // 配置列表合法的缩进空格为 4
    "MD007": { "indent": 4 },
    "no-hard-tabs": false
}
```

要扩展另一个配置文件，这样的文件可以使用 extends 属性来提供相对路径：

```json
{
    "extends": "../.markdownlint.json",
    "no-hard-tabs": true
}
```

通过 extends 引用的文件不需要是当前项目的一部分（但通常是）。还可以使用 Code 对 [用户和工作区的设置](https://code.visualstudio.com/docs/customization/userandworkspace) 来配置规则。

上述配置在 Code 的用户设置文件(Setting.json)中可能如下所示：

```json
{
    "editor.someSetting": true,
    "markdownlint.config": {
        "default": true,
        "MD003": { "style": "atx_closed" },
        "MD007": { "indent": 4 },
        "no-hard-tabs": false
    }
}
```

用户设置(Setting.json)中的扩展引用的文件路径是相对于用户的主目录解析的（例如，Windows 上的 `%USERPROFILE%` 或 macOS/Linux 上的 `$HOME`）。工作空间设置中的扩展引用的文件路径相对于工作空间文件夹进行解析。工作空间内的扩展引用的文件路径是相对于文件本身解析的。

配置源具有以下优先级（按降序排列）：

- 在同一或父目录中的 `.markdownlint-cli2.{jsonc,yaml,js}` 文件
- 在同一或父目录中的 `.markdownlint.{jsonc,json,yaml,yml,js}` 文件
- Visual Studio Code 用户/工作区设置
- 默认配置（见上文）

保存到任何位置的配置更改会立即生效。通过扩展引用的文件不会被监控更改。可以在任何配置文件中显式禁用（或重新启用）继承的配置。

当工作区打开时，运行 `markdownlint.openConfigFile` 命令将打开在工作区的根目录下的 `.markdownlint.{jsonc,json,yaml,yml,js}` 配置文件。如果这些文件都不存在，包含默认规则配置的新 .markdownlint.json 将在编辑器中以“等待保存”状态打开。

#### 1.1.5.2. markdownlint.focusMode

默认情况下，所有 linting 问题都会在您键入或编辑文档时被记录并突出显示。这包括诸如 MD009/无尾随空格之类的“瞬态”问题，如果您发现这让人分心，可以将 linting 配置为忽略光标所在行的问题。这在 Code 的用户设置中如下所示：

```json
{
    "editor.someSetting": true,
    "markdownlint.focusMode": 2
}
```

面示例中的值 2 将忽略光标所在行、光标上方的 2 行和光标下方的 2 行的问题。

> 注：这是一个应用程序级设置，仅在用户（而非工作区）设置中有效。

#### 1.1.5.3. markdownlint.run

默认情况下，linting 在您键入或编辑文档时执行。 Linting 快速高效，不应干扰典型的工作流程。如果您发现这让人分心，可以将 linting 配置为仅在保存文档时运行。这在 Code 的用户设置中如下所示：

```json
{
    "editor.someSetting": true,
    "markdownlint.run": "onSave"
}
```

> 注：当配置为运行 onSave 时，报告的问题列表将在编辑文档时过时，并在保存文档时更新。

#### 1.1.5.4. markdownlint.ignore

如果工作区包含生成的内容或其他触发警告但无法修复的 Markdown 文件，则可以通过配置在 linting 时忽略（跳过）这些告警。这可以通过在项目的根目录中创建一个名为 `.markdownlintignore` 的文件来完成，或者通过使用与相关文件名匹配的 glob 表达式数组更新用户/工作区配置的 `markdownlint.ignore` 设置来完成。

当使用 `.markdownlintignore` 文件（或覆盖它）时，文件的内容遵循 gitignore 的规则，可能类似于：

```bash
# Ignore Markdown files in the test directory
test/*.md
!test/except/this/one.md
```

使用 Code 的工作区配置通过 glob 忽略文件的示例：

```json
{
    "editor.someSetting": true,
    "markdownlint.ignore": [
        "ignore.md",
        "directory/ignore.md",
        "**/ignore.md",
        "**/*.md"
    ]
}
```

或者通过引用不同的文件来忽略文件：

```json
{
    "editor.someSetting": true,
    "markdownlint.ignore": ".gitignore"
}
```

用于匹配 `markdownlint.ignore` 数组值的 globbing 库是 [minimatch](https://github.com/isaacs/minimatch) 并启用了 `dot` 和 `nocomment` 选项。匹配区分大小写，路径相对于工作空间的根进行解析。目录分隔符是 `/`，即使在 Windows 上也是如此。

> 注：也可以通过 `.markdownlint-cli2.{jsonc,yaml,js}` 中的 ignores 属性忽略文件（以其他工具可以识别的方式）

#### 1.1.5.5. markdownlint.customRules

可以在 Code 的用户/工作区配置中指定自定义规则，以应用超出默认规则集的额外 linting。自定义规则由 JavaScript 文件的路径或导出一个规则或一组规则（[自定义规则示例](https://www.npmjs.com/search?q=keywords:markdownlint-rule)）的 npm 包的名称或路径指定。

路径通常是相对于当前工作空间的根目录（或当没有打开文件夹时用户的主目录），并且应该以 `./` 开头，[以区分相对路径和模块标识符](https://nodejs.org/dist/latest-v14.x/docs/api/modules.html#modules_file_modules)。路径可以是绝对的，并以 `/` 开头，尽管不鼓励这样做，因为它不能在不同的机器上可靠地工作。如果在工作区中实施自定义规则，请考虑在 `.vscode` 目录下提交规则代码，该目录将与其他工作区内容分开，并且可供克隆存储库的每个人使用。`{extension}/path` 形式的路径相对于名为 `extension` 的代码扩展的基目录（必须已安装）。此语法允许将自定义规则包含在另一个扩展的包中，尽管不鼓励这样做，因为它引入了对另一个扩展的微妙依赖。

Code 的自定义规则工作区设置示例可能如下所示：

```json
{
    "editor.someSetting": true,
    "markdownlint.customRules": [
        "./.vscode/my-custom-rule.js",
        "./.vscode/my-custom-rule-array.js",
        "./.vscode/npm-package-for-custom-rule",
        "/absolute/path/to/custom/rule.js",
        "{publisher.extension-name}/custom-rule.js",
        "{publisher.extension-name}/npm/rule/package"
    ]
}
```

有关编写自定义规则的信息，请参阅 [自定义规则的 markdownlint 文档](https://github.com/DavidAnson/markdownlint/blob/main/doc/CustomRules.md)。

> 注：还可以通过 `.markdownlint-cli2.{jsonc,yaml,js}` 中的 `customRules` 属性指定自定义规则（以其他工具可以识别的方式）

#### 1.1.5.6. markdownlint.lintWorkspaceGlobs

linting 工作区时使用的标准 glob 应该与 VS Code 的“重要的 Markdown 文件”的默认概念相匹配：

```json
[
    // Source: https://github.com/microsoft/vscode/blob/main/extensions/markdown-basics/package.json
    "**/*.{md,mkd,mdwn,mdown,markdown,markdn,mdtxt,mdtext,workbook}",
    // Source: https://github.com/microsoft/vscode/blob/main/src/vs/workbench/contrib/search/browser/search.contribution.ts
    "!**/node_modules",
    "!**/bower_components",
    // Additional exclusions
    "!**/.git"
]
```

可以在工作区或用户范围内自定义此列表，以包含和排除其他文件和目录。有关语法的更多信息，请参阅 [markdownlint-cli2 文档的“命令行”部分](https://github.com/DavidAnson/markdownlint-cli2#command-line)。

### 1.1.6. 抑制告警

可以使用 Markdown 文件本身中的注释来抑制单个警告：

```xml
<!-- markdownlint-disable MD037 -->
deliberate space * in * emphasis
<!-- markdownlint-enable MD037 -->
```

有关内联抑制的更多信息可以在 [markdownlint README.md 的配置部分](https://github.com/DavidAnson/markdownlint#configuration) 中找到。

### 1.1.7. Snippets

编辑 Markdown 文档时可以使用以下片段（按 `Ctrl+Space/⌃Space` 获取 IntelliSense 建议）：

- `markdownlint-disable`
- `markdownlint-enable`
- `markdownlint-disable-next-line`
- `markdownlint-capture`
- `markdownlint-restore`
- `markdownlint-disable-file`
- `markdownlint-enable-file`
- `markdownlint-configure-file`

### 1.1.8. 安全

从自定义规则、`markdown-it` 插件或配置文件（例如 `.markdownlint.cjs` 和 `.markdownlint-cli2.cjs`）运行 JavaScript 可能存在安全风险，因此 VS Code 的 Workspace Trust 设置能够阻止 JavaScript 用于不受信任的工作区。

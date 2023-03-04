# 1. Markdown + Math

- [1. Markdown + Math](#1-markdown--math)
  - [1.1. 官方文档](#11-官方文档)
    - [1.1.1. What is it](#111-what-is-it)
    - [1.1.2. What is new in mdmath 2.7.0](#112-what-is-new-in-mdmath-270)
    - [1.1.3. 基本功能](#113-基本功能)
    - [1.1.4. 安装](#114-安装)
      - [1.1.4.1. VSCode 安装该插件](#1141-vscode-安装该插件)
      - [1.1.4.2. 从 Mac 和 Linux 命令行中安装](#1142-从-mac-和-linux-命令行中安装)
      - [1.1.4.3. 从 Windows 命令行](#1143-从-windows-命令行)
    - [1.1.5. Usage](#115-usage)
    - [1.1.6. 支持的配置以及默认值](#116-支持的配置以及默认值)
    - [1.1.7. 依赖项](#117-依赖项)
    - [1.1.8. FAQ](#118-faq)

## 1.1. 官方文档

> 详见 Markdown+Math [官方文档](https://marketplace.visualstudio.com/items?itemName=goessner.mdmath)

### 1.1.1. What is it

*MdMath* 允许使用 Visual Studio Code 作为排版和渲染 *TeX math.K* 的编辑器。事实上它现在重用了内置的 Markdown viewer。 KaTeX 在内部作为一个快速的数学渲染器工作。

您可以直接从 [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=goessner.mdmath) 安装该扩展。

### 1.1.2. What is new in mdmath 2.7.0

- 现在在导出 HTML 时，可以选择的不同主题：
  - default
  - minimal
  - publication (LaTeX style)
- about LaTeX style publication theme:
  - view [HTML publication](https://goessner.github.io/mdmath/publication.html).
  - view [PDF publication](https://www.researchgate.net/publication/352151169_Web_Publications_-_LaTeX_Style)
  - Download [PDF paper](https://goessner.github.io/mdmath/publication.pdf)
- 支持Commutative diagrams
- 支持插入 TOC。通过从命令面板，运行命令 `Insert Table of Content` (Ctrl+K T) 在光标位置注入 ToC。
- 通过设置 `mdmath.silent` 为 false，可以禁用导出 HTML 时的用户通知。
- 通过设置 `mdmath.outerspace` 为 *true* (默认为：fasle，以实现向后兼容)，来强制在数据表达式声明符 $...$ 周围添加空格，解决渲染时错误解析符号 $ 的问题。

### 1.1.3. 基本功能

简化包含数学表达式的 Markdown 文档的创作以及支持实时预览。对于以 Markdown 为首选文档格式的科学家、工程师和学生来说，此扩展是一个合适的工具。

- 基于 [markdown-it](https://github.com/markdown-it/markdown-it) 插件 [markdown-it-texmath](https://github.com/goessner/markdown-it-texmath).
- 由于 markdown-it-texmath 支持不同的公式分隔符，这些也可用并且用户可以使用 mdmath 进行配置：
  - `dollars`(默认)
    - 行内公式：`$...$`
    - 多行公式：`$$...$$`
    - 多行公式 + 方程编号：`$$...$$ (1)`
  - `brackets`
    - 行内公式：`\(...\)`
    - 多行公式：`\[...\]`
    - 多行公式 + 方程编号：`\[...\] (1)`
  - `gitlab`
    - 行内公式：``$`...`$``
    - 多行公式：`` ```math...``` ``
    - 多行公式 + 方程编号：`` ```math...``` (1) ``
  - `julia`
    - 行内公式：`$...$` 或 ` ``...`` `
    - 多行公式：`` ```math...``` ``
    - 多行公式 + 方程编号：`` ```math...``` (1) ``
  - `kramdown`
    - 行内公式：`$$...$$`
    - 多行公式：`$$...$$`
    - 多行公式 + 方程编号：`$$...$$ (1)`

### 1.1.4. 安装

#### 1.1.4.1. VSCode 安装该插件

在 Visual Studio Code 中进入扩展商店，键入扩展名，然后从列表中选择 Markdown+Math 扩展。

#### 1.1.4.2. 从 Mac 和 Linux 命令行中安装

```bash
cd $HOME/.vscode/extensions
git clone https://github.com/goessner/mdmath.git
cd mdmath
npm install
```

#### 1.1.4.3. 从 Windows 命令行

```bash
cd  %USERPROFILE%\.vscode\extensions
git clone https://github.com/goessner/mdmath.git
cd mdmath
npm install
```

### 1.1.5. Usage

- 启动 VS Code，创建或打开 Markdown 文件 (.md)。
- 打开预览窗口。
- 在 Markdown 源窗口中排版并查看预览窗口实时更新。
- 按 `Ctrl+K ,` ，或运行命令 `Save Markdown+Math to HTML` 将对应的 HTML 源代码保存到文件系统。
- 按 `Ctrl+K .` 。或者运行命令 `Clip Markdown+Math to HTML` 将对应的 HTML 源代码复制到底层系统剪贴板。
- 按 `Ctrl+K T` 或运行命令 `Insert Table of Content` 以在光标位置插入生成的目录。

### 1.1.6. 支持的配置以及默认值

```json
  "mdmath.delimiters": "dollars",
  "mdmath.macros": {},
  "mdmath.macroFile": "",
  // 指定导出的 HTML 文件的输出路径
  "mdmath.savePath": "./${file.name}.html",
  // autosave 如果设置为 ture，每当您保存 markdown 文件时，也会保存为对应的 Html 文件
  "mdmath.autosave": false,
  "mdmath.style": "",
  "mdmath.theme": "default",
  "mdmath.silent": false,
  "mdmath.outerspace": false
```

### 1.1.7. 依赖项

- [markdown-it](https://github.com/markdown-it/markdown-it): VSCode 中的 markdown 渲染器。
- [katex](https://github.com/Khan/KaTeX): 在 HTML 中快速渲染 TeX 公式。

### 1.1.8. FAQ

**Q1: 如何让导出的 HTML 使用自定义的 CSS 文件？**

- A: 通过设置 `mdmath.style` 将其定义为 **绝对 URL**。例如，您可以设置为 `"mdmath.style": "file://c:/mystyle/mystyle.css"`。

**Q2: 如何定义和使用宏？**

- 在用户设置中定义它们。例如：

```json
"mdmath.macros": {
    "\\RR": "\\mathbb{R}",
    "\\vek": "{\\begin{pmatrix}#1\\\\#2\\end{pmatrix}}"
}
```

- 在您的 Markdown 文档中使用它们。例如：

```json
Vectors in $\RR^2$ have a shape of

$$\vek{x}{y}$$
```

**Q3: 如何在文件中定义宏？**

- 创建一个包含宏的 JSON 文件并在用户设置中定义其路径。例如:

```json
"mdmath.macroFile": "c:/myfiles/mymacros.json"
```

- 以与用户设置相同的方式定义宏。
- 用户宏定义文件优先于用户定义的宏设置，如果冲突，后者将会被忽略。

**Q4: 是否有全局预定义宏？**

- 没有。宏是用户设置 `mdmath.macros` 定义的。因此它们在所有用户特定的 Markdown 文档中都可用。

**Q5: KaTeX 支持哪些功能？**

- 请参阅 [KaTeX Supported Functions](https://khan.github.io/KaTeX/docs/supported.html) 和 [KaTeX Support Table](https://katex.org/docs/support_table.html)

**Q6: 内联公式有什么限制？**

- 第一个 `$` 之后和第二个 `$` 之前的空格是不允许的
- 第一个 `$` 之前和第二个 `$` 之后的数字字符是不允许的
- 两个连续的内联公式之间至少需要一个字符（比如空格）进行分割
- 内部不允许换行

**Q7: 多行公式有什么限制？**

- 不允许内联文本。
- 不能用在表格内部，表格内部应用内联公式代替。
- 需要前后空行。
- 内联公式的限制不适用

**Q8: 我可以为预览窗口使用自定义 CSS 样式吗？**

- 通过设置 `mdmath.style` 将其定义为 **绝对 URL**。例如，您可以设置为 `"mdmath.style": "file://c:/mystyle/mystyle.css"`。

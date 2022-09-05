# 1. 自动生成 Python 的注释

Table of Contents

- [1. 自动生成 Python 的注释](#1-自动生成-python-的注释)
  - [1.1. 配置生成文件头的注释](#11-配置生成文件头的注释)
  - [1.2. 安装生成函数注释的插件](#12-安装生成函数注释的插件)
    - [1.2.1. 用法](#121-用法)
    - [1.2.2. 扩展设置](#122-扩展设置)
    - [1.2.3. 自定义文档字符串模板](#123-自定义文档字符串模板)
  - [1.3. 参考链接](#13-参考链接)

## 1.1. 配置生成文件头的注释

## 1.2. 安装生成函数注释的插件

推荐插件 [autoDocstring - Python Docstring Generator](https://marketplace.visualstudio.com/items?itemName=njpwerner.autodocstring)。该插件用于快速生成 *python* 函数的文档字符串。

功能：

- 快速生成可以通过标签浏览的文档字符串片段。
- 提供多种不同类型的文档字符串格式以供选择
- 通过 *pep484* 类型提示、默认值和 var 名称推断参数类型。
- 支持 args、kwargs、装饰器、错误和参数类型

支持的注释 (文档字符串) 格式：

- [google](https://github.com/NilsJPWerner/autoDocstring/blob/HEAD/docs/google.md)
- [sphinx](https://github.com/NilsJPWerner/autoDocstring/blob/HEAD/docs/sphinx.md)
- [numpy](https://github.com/NilsJPWerner/autoDocstring/blob/HEAD/docs/numpy.md)
- [docBlockr](https://github.com/NilsJPWerner/autoDocstring/blob/HEAD/docs/docblockr.md)
- [one-line-sphinx](https://github.com/NilsJPWerner/autoDocstring/blob/HEAD/docs/one-line-sphinx.md)
- [pep257](https://github.com/NilsJPWerner/autoDocstring/blob/HEAD/docs/pep257.md)

要关闭文档字符串中的类型生成，请使用所需格式的 `-notypes` 模板。

> docBlockr 格式是 *PEP0257* 的类型化版本。

### 1.2.1. 用法

光标必须位于定义正下方的行上才能生成完整的自动填充的文档字符串：

- 方法1：使用三引号打开文档字符串后按回车键（可配置 `"""` 或 `'''`）
- 方法2：键盘快捷键： `ctrl+shift+2` 或 `cmd+shift+2` (for mac)
  - 可以在`Preferences -> Keyboard Shortcuts -> extension.generateDocstring` 中更改
- 在命令面板中使用命令：`Generate Docstring`
- 右键菜单：`Generate Docstring`

### 1.2.2. 扩展设置

此扩展提供以下设置：

- `autoDocstring.docstringFormat`：在不同的文档字符串格式之间切换
- `autoDocstring.customTemplatePath`：自定义文档字符串模板的路径（绝对或相对于项目根目录）
- `autoDocstring.generateDocstringOnEnter`：打开文档字符串后按回车生成文档字符串
- `autoDocstring.includeExtendedSummary`：在文档字符串中包含扩展摘要部分
- `autoDocstring.includeName`：在文档字符串的开头包含函数名
- `autoDocstring.startOnNewLine`：摘要占位符前的新行
- `autoDocstring.guessTypes`：从类型提示、默认值和变量名推断类型
- `autoDocstring.quoteStyle`：文档字符串的引号样式

### 1.2.3. 自定义文档字符串模板

此扩展现在支持自定义模板。该扩展使用 `mustache.js` 模板引擎。要使用自定义模板，请创建一个 `.mustache` 文件并使用 `customTemplatePath` 配置指定其路径。查看包含的 *google* 文档字符串模板以获取使用示例。以下标签可用于自定义模板。

Variables:

```txt
{{name}}                        - name of the function
{{summaryPlaceholder}}          - _summary_ placeholder
{{extendedSummaryPlaceholder}}  - [extended_summary] placeholder
```

Sections:

```txt
{{#args}}                       - iterate over function arguments
    {{var}}                     - variable name
    {{typePlaceholder}}         - _type_ or guessed type  placeholder
    {{descriptionPlaceholder}}  - _description_ placeholder
{{/args}}

{{#kwargs}}                     - iterate over function kwargs
    {{var}}                     - variable name
    {{typePlaceholder}}         - _type_ or guessed type placeholder
    {{&default}}                - default value (& unescapes the variable)
    {{descriptionPlaceholder}}  - _description_ placeholder
{{/kwargs}}

{{#exceptions}}                 - iterate over exceptions
    {{type}}                    - exception type
    {{descriptionPlaceholder}}  - _description_ placeholder
{{/exceptions}}

{{#yields}}                     - iterate over yields
    {{typePlaceholder}}         - _type_ placeholder
    {{descriptionPlaceholder}}  - _description_ placeholder
{{/yields}}

{{#returns}}                    - iterate over returns
    {{typePlaceholder}}         - _type_ placeholder
    {{descriptionPlaceholder}}  - _description_ placeholder
{{/returns}}
```

Additional Sections:

```txt
{{#argsExist}}          - display contents if args exist
{{/argsExist}}

{{#kwargsExist}}        - display contents if kwargs exist
{{/kwargsExist}}

{{#parametersExist}}    - display contents if args or kwargs exist
{{/parametersExist}}

{{#exceptionsExist}}    - display contents if exceptions exist
{{/exceptionsExist}}

{{#yieldsExist}}        - display contents if returns exist
{{/yieldsExist}}

{{#returnsExist}}       - display contents if returns exist
{{/returnsExist}}

{{#placeholder}}        - makes contents a placeholder
{{/placeholder}}
```

## 1.3. 参考链接

- [1] Nils Werner.[autoDocstring - Python Docstring Generator](https://marketplace.visualstudio.com/items?itemName=njpwerner.autodocstring) [j].marketplace.visualstudio.com

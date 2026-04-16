---
name: typst-author-chinese
description: 生成符合中文排版习惯的 Typst（.typ）代码，编辑、调试 Typst 文档与项目，回答 Typst 语法与参考问题。当用户处理 .typ 文件、涉及 Typst 文档创建/编辑/调试/编译/格式化/模板/包的使用，或者涉及中文排版、中文学术论文、中文书籍排版、CTeX 替代、中文字体配置、中文标点处理等场景时，均应使用本 skill。也适用于任何 Typst 语法参考和项目构建需求。
---

# typst-author skill（中文排版适配版）

## Overview

本 skill 帮助智能体生成、编辑和处理 Typst 文档，特别针对中文排版需求进行了适配。提供了中文排版快速入门示例、详细工作流，以及指向完整 Typst 文档（指南、教程、参考）的链接。

## Minimal document example（中文文档）

```typst
#set document(title: "我的文档", author: "作者姓名")
#set page(numbering: "1")
#set text(lang: "zh", font: ("New Computer Modern", "Noto Serif CJK SC"))

// 中文段落首行缩进两个字符
#set par(first-line-indent: 2em, justify: true)
#show par: set block(spacing: 0.75em)

// 中文标题
#title[我的文档]

= 第一章

这是一段中文正文。Typst 对中文排版有良好的原生支持。

== 第一节

中文排版需要注意以下要点：字体选择、标点挤压、首行缩进以及行距设置。
```

## Workflows

- **创建新的 Typst 项目**：以"Minimal document example"为起点。阅读教程基础部分（[docs/tutorial/writing-in-typst.md](docs/tutorial/writing-in-typst.md)），然后创建 `.typ` 文件。每次编辑后，若 `typstyle` 可用，执行下方格式化检查。
- **编辑已有内容**：定位目标文本并修改；需要时对照参考文档确认语法（[docs/reference/](docs/reference/)）。修改 `.typ` 文件后执行格式化检查。
- **排版与样式**：参考样式指南（[docs/reference/styling.md](docs/reference/styling.md)）了解 `set rule`、`show rule` 和自定义主题。

## Documentation

- **语法与基础**：`docs/reference/syntax.md`
- **样式与 show/set 规则**：`docs/reference/styling.md`
- **脚本与运行时行为**：`docs/reference/scripting.md`
- **页面设置与表格**：`docs/guides/page-setup.md` 和 `docs/guides/tables.md`
- **面向任务的排版帮助**：`docs/tutorial/writing-in-typst.md`、`docs/guides/*.md` 和 `docs/reference/**/*.md`

## Detailed instructions

1. **优先使用本地文档**。你对 Typst 的内部训练数据可能过时或不准确。在生成代码之前，务必根据本地 `docs/` 文件夹核实函数名、参数和语法。
2. **阅读相关文档**，使用本地文件搜索和打开工具查阅上述路径。
3. **使用本地文档回答语法和参考问题**。从打包文档中核实语法、函数名、参数和参考行为。仅在查阅文档后仍无法确定运行时行为时，才运行最小的 Typst 探测。
4. **根据用户请求生成或修改 `.typ` 源文件**。
5. **对每次创建或编辑的 `.typ` 文件执行下方格式化检查**。
6. **在格式化决策完成后**，当你创建或编辑了 `.typ` 文件，或用户明确要求验证时，用 `typst compile` 验证（如果工具有权限）。
7. **总结已修改的文件和结果**。仅在用户请求或无法直接编辑时提供完整 `.typ` 内容，可选附带渲染预览（PDF/HTML）。

### 中文排版专项指引

Typst 对中文排版有良好的原生支持。以下是中文排版的关键注意事项：

1. **语言设置**：始终使用 `#set text(lang: "zh")` 开启中文排版模式，这将自动启用中文标点挤压和断行规则。
2. **字体配置**：Typst 的字体回退机制会为 CJK 字符选择合适的字体。显式指定中文字体可确保一致性：
   ```typst
   #set text(font: ("New Computer Modern", "Noto Serif CJK SC"))
   ```
   常用中文字体：`Noto Serif CJK SC`（宋体风格）、`Noto Sans CJK SC`（黑体风格）、`Source Han Serif SC`（思源宋体）、`Source Han Sans SC`（思源黑体）。
3. **首行缩进**：中文排版惯例要求段落首行缩进两个字符：
   ```typst
   #set par(first-line-indent: 2em)
   ```
   注意：Typst 会自动在标题、列表等元素后的第一个段落跳过缩进。
4. **行距与段距**：中文排版通常使用较大的行距和段距：
   ```typst
   #set par(leading: 1em)
   #show par: set block(spacing: 0.75em)
   ```
5. **标点处理**：`lang: "zh"` 会自动处理中文标点挤压（如"》、《"之间的间距调整）。如需更细粒度控制，参考 `docs/reference/text.md`。
6. **页面尺寸**：中文文档常使用 A4 或 16 开纸张，边距可根据排版需求调整。
7. **中英混排**：Typst 会在中英文之间自动插入小间距。无需手动处理。
8. **目录与编号**：中文文档的章节编号可使用中文数字或阿拉伯数字：
   ```typst
   #set heading(numbering: "一、")
   ```

### 探测不确定行为

- 当打包文档无法确定运行时或求值行为时使用探测。
- 按照 [docs/reference/scripting.md](docs/reference/scripting.md) 中的描述，使用 Typst 脚本建模。
- 需要探测时，优先通过 stdin 进行无文件探测，而非创建临时 `.typ` 文件。使用 `metadata(...) <probe>` 暴露值，用 `typst query - "<probe>" --field value --one` 读取。参见 [docs/reference/introspection/query.md](docs/reference/introspection/query.md) 和 [docs/reference/introspection/metadata.md](docs/reference/introspection/metadata.md)。
- 示例：`printf '#metadata(1 + 2) <probe>\n' | typst query - "<probe>" --field value --one`

### 编辑后格式化检查

1. 用 `command -v typstyle` 检查 `typstyle` 是否可用。若不可用，跳过剩余格式化检查。
2. **每次修改 `.typ` 文件后，运行 `typstyle --check <file>`**。
3. **若 `typstyle --check` 失败，先用 `typstyle --diff <file>` 检查格式化变更**，再决定如何处理。
4. **仅当格式化变更限于新创建的文件或当前任务中你编辑的代码时，使用 `typstyle -i <file>` 应用格式化**。
5. **当格式化会影响未修改的已有代码时，停下来询问用户**。如果 diff 超出你的编辑范围，或者无法确认每个格式化变更仅限于你的编辑，应询问而非格式化。

## Quick syntax reference

### 关键区别

- **数组**：`(item1, item2)`（圆括号）。参见 [docs/reference/foundations/array.md](docs/reference/foundations/array.md)。
- **字典**：`(key: value, key2: value2)`（带冒号的圆括号）。参见 [docs/reference/foundations/dictionary.md](docs/reference/foundations/dictionary.md)。
- **内容块**：`[markup content]`（方括号）。参见 [docs/reference/foundations/content.md](docs/reference/foundations/content.md)。
- **没有元组**：Typst 只有数组。

### `#` 号用法（标记模式 vs 代码模式）

- 在标记模式或内容块中，用 `#` 开启代码表达式；它将代码与文本区分开来。在标记模式中，产生内容的函数调用和字段访问必须加 `#`：`#figure[...]`、`#image("file.png")`、`text(...)[#numbering(...)]`。
- 在代码上下文中（参数列表、代码块、show 规则体）不要使用 `#`。示例：`#figure(image("file.png"))`（`image` 前不加 `#`）。
- 参考：[docs/reference/scripting.md](docs/reference/scripting.md)、[docs/tutorial/writing-in-typst.md](docs/tutorial/writing-in-typst.md)

```typst
// 错误（内容块中缺少 #）
text(...)[(numbering(...))]

// 正确
text(...)[(#numbering(...))]
```

### 样式规则：set vs show

- `set`：设置规则，用于配置元素函数的可选参数（样式默认值，作用域限定为当前块或文件）。
- `show`：显示规则，用于选定目标元素并应用设置规则或变换/替换元素输出。
- 常规样式用 `set`；选择性或结构性变更用 `show`（例如 `heading.where(level: 1)`、标签、文本、正则）。

```typst
// 设置规则：配置元素类型的可选参数
#set heading(numbering: "I.")
#set text(font: "New Computer Modern")

// show-set 规则：仅对选定元素应用设置规则
#show heading: set text(navy)

// show 变换规则：替换/重塑元素输出
#show heading: it => block[#emph(it.body)]
```

## Common mistakes to avoid

- 把 Typst 数组称为"元组"（Typst 只有数组，没有元组）。
- 用 `[]` 表示数组（应使用 `()`）。
- 用 `arr[0]` 访问数组元素（应使用 `arr.at(0)`）。
- 在标记/内容块中遗漏 `#`（如 `text(...)[numbering(...)]` 应为 `text(...)[#numbering(...)]`）。
- 在代码上下文中使用 `#`（如参数列表中 `figure(#image("x.png"))`）。
- 混淆内容块 `[]` 与代码块 `{}`。
- 访问导入的变量/函数时遗漏命名空间（如应使用 `color.hsl` 而非 `hsl`）。
- 使用 LaTeX 语法（**不要**使用 `\begin{...}`、`\section` 等 LaTeX 命令）。
- 凭空臆造不存在的环境（如 `tabular` 不存在，应使用 `table`）。
- 中文文档中忘记设置 `lang: "zh"`，导致标点挤压和断行规则不生效。
- 中文文档中遗漏首行缩进设置。

## Advanced features

- **自定义主题**：参见 [docs/reference/styling.md](docs/reference/styling.md)。
- **脚本编程**：使用 Typst 脚本能力（[docs/reference/scripting.md](docs/reference/scripting.md)）进行自动生成。
- **数学与可视化**：参考 [docs/reference/math/](docs/reference/math/) 和 [docs/reference/visualize/](docs/reference/visualize/)。

### 大型项目

处理大型项目时，考虑将项目拆分为多个文件。

- 使用 `#include "file.typ"` 拆分多个文件
- 相关文档：[docs/reference/foundations/module.md](docs/reference/foundations/module.md)

## Troubleshooting

### 字体缺失警告

若出现"unknown font family"警告，移除字体指定以使用系统默认字体。注意：字体警告不会阻止编译，文档将使用回退字体。

### 模板/包未找到

若导入失败并提示"package not found"：

- 在 Typst Universe 上核实确切的包名和版本号。
- 检查 `@preview/package:version` 语法中的拼写错误。

### 编译错误

常见修复：

- **"expected content, found ..."**：在需要标记的地方使用了代码——用 `#{ }` 包裹或使用正确语法。
- **"expected expression, found ..."**：标记/内容块中缺少 `#`（或 `#(...)`）。
- **"unknown variable"**：检查拼写，确保导入正确。
- **数组/字典错误**：检查语法——两者都用 `()`，字典需要 `key: value`，单元素数组写为 `(elem,)`。

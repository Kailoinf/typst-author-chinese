# typst-author-chinese

Typst 中文排版 SKILL。This is an agent skill designed for the purpose of authoring documents utilising native Chinese typography. 

## 安装

### Claude Code

```bash
# 方式一：marketplace（推荐）
claude plugin marketplace add gakusyun/typst-author-chinese
claude plugin install typst-author-chinese@typst-author-chinese

# 方式二：手动安装（源码）
git clone https://github.com/Gakusyun/typst-author-chinese.git ~/.claude/plugins/typst-author-chinese
```

重启 Claude Code，skill 将自动激活。

### OpenAI Codex CLI

```bash
git clone https://github.com/Gakusyun/typst-author-chinese.git ~/.codex/skills/typst-author-chinese
```

### 其他平台

本 skill 遵循 [Agent Skills 开放标准](https://agentskills.io/specification)，支持 Claude Code、Codex CLI、Cursor、Kiro、CodeBuddy、OpenClaw 等主流 AI Coding 工具。将本项目克隆到对应平台的 skills 目录即可。

## 功能

- 生成、编辑、调试 Typst（`.typ`）文档
- 中文排版专项支持：字体配置、首行缩进、标点挤压、中英混排
- 内置完整 Typst 参考文档（语法、样式、脚本、数学等）
- 编译验证（需 `typst`）

## 使用示例

### 1. 基础文档生成
```
# 创建一个新的 Typst 文档
let example = {
  #set text(font: "SimSun")
  #set par(first-line-indent: 2em)
  
  = 中文文档示例
  这是一个使用 Typst 编写的中文文档示例。
  
  本示例展示了：
  - 中文字体设置
  - 段落首行缩进
  - 中英混排优化
  
  Hello, world! 这是一段中英混合文本。
}
```

### 2. 表格创建
```
# 创建中文表格
let table-example = {
  #table(
    columns: 3,
    rows: 4,
    align: center,
    ..table.cell("姓名"),
    ..table.cell("年龄"),
    ..table.cell("专业"),
    ..table.cell("张三"),
    ..table.cell("25"),
    ..table.cell("计算机科学"),
    ..table.cell("李四"),
    ..table.cell("28"),
    ..table.cell("软件工程"),
    ..table.cell("王五"),
    ..table.cell("30"),
    ..table.cell("数据科学"),
  )
}
```

### 3. 数学公式排版
```
# 中文数学文档
let math-example = {
  #set text(font: "SimSun")
  #set math(font: "Cambria Math")
  
  $ 这是一个数学公式：$
  $ x = \frac{a + b}{c} $
  
  $ 中文数学文档通常需要中文字体与数学字体分离 $
}
```

### 4. 参考文献管理
```
# 中文参考文献
let bibliography = {
  #bibliography(
    style: "apa",
    data: (
      (key: "zhang2019", title: "深度学习在中文文本分类中的应用", author: "张三", year: 2019),
      (key: "li2020", title: "中文自然语言处理的最新进展", author: "李四", year: 2020),
    ),
  )
}
```

## 验证命令

```bash
# 编译验证（需要 typst）
typst compile <file.typ>
```

## 项目结构

```
typst-author-chinese/
├── SKILL.md              # skill 入口文件
├── CLAUDE.md             # Claude Code 开发指南
├── docs/                 # Typst 官方参考文档（只读）
│   ├── tutorial/         # 教程
│   ├── guides/           # 指南（页面设置、表格等）
│   └── reference/        # API 参考
└── references/           # 中文排版参考（可编辑）
    ├── font.md           # 字体配置
    ├── spacing.md        # 行距段距
    ├── first-line-indent.md
    ├── heading-numbering.md
    ├── table.md
    ├── math.md
    ├── figure.md
    ├── page.md
    ├── list.md
    └── bibliography.md
```

## 致谢

本项目基于 [typst-skills](https://github.com/apcamargo/typst-skills) 改编，增加了中文排版适配。

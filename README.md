# typst-author-chinese

一个面向中文排版的 Typst 智能体 skill，帮助 AI 助手生成符合中文排版习惯的 Typst 文档。

## 功能

- 生成、编辑、调试 Typst（`.typ`）文档
- 中文排版专项支持：字体配置、首行缩进、标点挤压、中英混排
- 内置完整的 Typst 参考文档（语法、样式、脚本、数学等）
- 自动格式化检查（需 `typstyle`）
- 编译验证（需 `typst`）

## 安装

将本仓库克隆到你的 skill 目录中：

```bash
git clone https://github.com/Gakusyun/typst-author-chinese.git
```

然后在你的智能体配置中指向本仓库路径，确保 `SKILL.md` 能被正确加载。

## 使用方法

在支持 skill 的 AI 编程助手（如 Claude Code）中，当你提出与 Typst 或中文排版相关的需求时，skill 会自动激活。例如：

- "帮我用 Typst 写一篇中文论文"
- "把这个 .typ 文件改成 A4 纸张并设置首行缩进"
- "Typst 里怎么设置中文宋体字体？"
- "帮我把这个 LaTeX 文档迁移到 Typst"

## 文档结构

```
typst-author-chinese/
├── SKILL.md          # skill 定义文件（入口）
├── docs/             # Typst 参考文档
│   ├── tutorial/     # 教程
│   ├── guides/       # 指南（页面设置、表格等）
│   └── reference/    # API 参考
└── README.md
```

## 依赖

- [Typst](https://typst.app) — 文档编译（可选，用于验证）
- [typstyle](https://github.com/typstyle-rs/typstyle) — 代码格式化（可选）

## 致谢

本项目基于 [typst-skills](https://github.com/apcamargo/typst-skills) 改编，增加了中文排版适配。

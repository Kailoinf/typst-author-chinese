# 首行缩进

中文排版要求段落首行缩进两个字符：

```typst
#set par(first-line-indent: (amount: 2em, all: true))
```

⚠️ **必须加 `all: true`**：不加则标题后的第一段不缩进。默认行为是标题后首段不缩进（西文排版习惯），`all: true` 强制所有段落都缩进。

如果只想让标题后缩进（其他元素后不缩进），不要用 `all: true`，而是对特定元素单独处理。

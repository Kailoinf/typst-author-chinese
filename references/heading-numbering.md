# 标题与编号

Typst 内置 `numbering()` 支持多种计数符号：`1` `a` `A` `i` `I` `一` `壹` 等，无需第三方包。

## 常用编号模式

```typst
// 阿拉伯数字多级
#set heading(numbering: "1.1")        // 1  / 1.1  / 1.1.1

// 中文数字 + 顿号
#set heading(numbering: "一、")        // 一、/ 二、/ 三、

// 罗马数字
#set heading(numbering: "I.")          // I. / II. / III.
```

## 混合编号：一级"第X章"、其余阿拉伯

用自定义函数按层级切换模式：

```typst
#set heading(numbering: (..nums) => {
  let ns = nums.pos()
  if ns.len() == 1 { numbering("第一章", ..ns) }
  else { numbering("1.1", ..ns) }
})
// 效果：第一章 / 1.1 / 1.1.1 / 第二章 / 2.1
```

## 编号模式语法

模式由 **前缀 + 计数符号 + 后缀** 组成。计数符号被实际数字替换，前缀后缀原样显示。多级时最后一个计数符号及其前缀自动重复。

```typst
#numbering("1.1)", 1, 2)    // 1.2)
#numbering("第一章", 3)       // 第三章
#numbering("I – 1", 12, 2)   // XII – 2
```

## 嵌套 emph/strong 样式

```typst
#show strong: it => {
  show emph: set text(green)
  it
}
#show emph: it => {
  show strong: set text(blue)
  it
}
```

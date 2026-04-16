# 标题与编号

## 中文数字编号

```typst
#set heading(numbering: "一、")
```

## 多级不同编号格式（numbly）

```typst
#import "@preview/numbly:0.1.0": numbly
#set heading(numbering: numbly(
  "第{1}章",    // 一级：第1章
  "{1}.{2}",    // 二级：1.1
  "({3:a})",    // 三级：(a)
))
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

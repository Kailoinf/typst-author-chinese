# 间距

## 行距

行高 = leading + 文字尺寸。中文黄金行高为字号 1.5–1.75 倍。

```typst
// 小四号（12pt）正文：行高约 20pt
#set par(leading: 0.67em)

// 五号（10.5pt）正文：行高约 17pt
#set text(size: 10.5pt)
#set par(leading: 0.62em)
```

设置 `top-edge` / `bottom-edge` 使文字外框更接近中文习惯：

```typst
#set text(top-edge: "ascender", bottom-edge: "descender")
```

## 段距

段间距 > 行高，清晰区分段落。不要用空行控制段距。

```typst
#set par(spacing: 0.75em)
// 标题段前段后距
#show heading.where(level: 1): set block(above: 24pt, below: 18pt)
#show heading.where(level: 2): set block(above: 12pt, below: 6pt)
```

⚠️ `#show par: set block(spacing: ..)` 在 Typst 0.12+ 已废弃，用 `#set par(spacing: ..)`。

## 两端对齐

```typst
#set par(justify: true)
```

中文方块字必须两端对齐，右侧参差不齐破坏版面。

## 字距

正文用默认。短标题可加宽（≤3pt）：

```typst
#show heading.where(level: 1): set text(tracking: 1.5pt)
```

## 行内公式与中文间距

Typst 不自动在行内公式与中文间插入间距：

```typst
#show math.equation.where(block: false): it => {
  h(0.25em, weak: true) + it + h(0.25em, weak: true)
}
```

## 代码块两端对齐

Typst 0.13+ 已默认修复。旧版本：

```typst
#show raw.where(block: true): set par(justify: false)
```

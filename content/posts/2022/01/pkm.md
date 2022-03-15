---
title: "Obsidian、Logseq 还不够好"
date: 2022-01-27T16:15:45+08:00
draft: false
---

我用的笔记软件是 [TiddlyWiki](https://tiddlywiki.com/)，已经用了 6 年多，写了 1500+ 条目；公开的部分放在 [这里](https://wiki.zhiheng.io/)。

近几年 Obsidian 及 Logseq 大火，经常被人提及，于是我也尝试了下，但觉得他们都不够好。

## Obsidian

Obsidian 跟 TiddlyWiki 的定位很像，也是结构化的笔记软件（带目录树、tag 等）。

Obsidian 对比 TW 的优势，主要在于 **编辑体验**：

* [Advanced Tables Toolbar](https://github.com/tgrosinger/advanced-tables-obsidian) 插件，写表格简直太爽了
* 按 <kbd>Cmd-E</kbd> 可以切换编辑态和预览态，还会记得你上次编辑的光标位置，非常实用
* Paste URL into selection，这个功能非常实用，VSCode 的 Markdown 编辑器也有
* 有方便的 command palette

Obsidian 的不足在于：

* **默认排版差**，糟糕的 typography 和配色
* **UX 差**，难用，缺乏逻辑。这点抄下 VSCode 多好
* **仍不稳定**，我调整过某一主题的 CSS，但是在 Obsidian 升级版本后，一些 style 又被改变了
* **Publish 服务收费**，而且很贵
* **搜索功能缺乏想象力**，既然有了 file-level metadata（YAML front matter），为啥不能根据 metadata 做搜索？

总而言之，如果把 Obsidian 作为结构化笔记软件使用的话，我觉得 TiddlyWiki 体验更佳。

## Logseq

Logseq 跟 TiddlyWiki 并不是一类笔记软件。Logseq 底层用的是图数据库，是为了实现更灵活的编程能力设计的；它并不注重内容的结构化。

我不喜欢 Logseq 的最大问题是，它的排版不好（即使有高质量的仿 bear 主题），编辑起来也不顺手。它在设计上用了 block 来替代段落的作用，但 block 又跟 unordered list 有千丝万缕的关系，用起来很不舒服。下面是一张截图：

![Logseq Bad Typography](/image/2022/01/logseq-bad-typography.png)

另外我并不是很需要这些核心能力：

* **block 级别的 reference 及 embed**：block 的确比 page 更细，但是 page 往往已经满足需求了
* **双向链接、page graph**：我不觉得有啥用。下面详谈
* **图数据库带来的高级查询能力**：这确实很棒。但用 TiddlyWiki 也能实现类似的能力

## 要不要给内容做分类？

双向链接带来一个 **假象**：我并不需要给内容做分类，只要开始写内容，再用链接把他们关联起来，就能将它融入自己知识体系中。

但人脑运作依赖归纳和分类，一旦你录入的内容到达一定的量，始终是需要去做分类的。即使是 Logseq 的 [帮助文档](https://logseq.github.io/) 也对内容做了分类。Logseq 在设计上缺乏对目录树的支持（两个 page 并没有父子关系）；你只能建一个索引页，再手工把一项项加进来，这很不好维护。

## 双向链接、Graph View 有用吗？

它们有帮到更深入地理解知识吗？

我并不是觉得链接不好。但是双向链接中比较新颖的部分——反向链接（back link），实在没什么作用。如果我需要 back link 才能联想起这些知识点的关系，那一定是我并没有真的理解它们。

至于 graph view，它除了是一块 fancy eye candy，还有其他的作用吗？

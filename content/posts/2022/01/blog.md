---
title: "2022 新博客"
date: 2022-01-25T00:12:32+08:00
draft: false
---

换了个新博客系统及主题。

## 起因

我的旧博客系统是基于 Jekyll 的，由 GitHub Pages 托管。

在我更新了旧博客后，GitHub Pages 就没法正常构建了；换成 Vercel 也一样不行。虽然旧博客在我的调优下排版已经比较 OK，但是想到 Jekyll 是基于 Ruby 的，我并没有兴趣去折腾 Ruby，索性就来看看有什么新工具可以选择。

## 我的需求

这次的新博客，倾向于做类似 [Happy Xiao][happy-xiao] 的短内容。在我看来：

- 零散的技术内容没有价值，它应该存放在你的笔记系统中
- 每篇内容把一个观点简练地阐述清楚，别人可以看得有趣，对自己思考也有帮助
- 多写才会有提高

因此，对于博客系统和主题，我期望：

- 系统使用足够简单
- 主题足够简单
- 排版足够美观

我不在乎：

- 主题有没有好看的 UI 设计
- 有没有头图、评论等锦上添花的功能

[happy-xiao]: https://happyxiao.com/

## 博客系统选择

有几种选择：

- **Next.js / Gatsby**：比较新潮的单页应用框架。但是新代表着折腾程度高，而且 JS 项目在不维护的情况下，时常过几个月就不能正常构建了，我并不想浪费这个时间去折腾
- **Hexo**：是专门做静态网站生成的。但是也是 JS 项目，有上一条一样的问题，我不想去折腾
- **Jekyll**：直观感受是很优雅，但是基于上面的原因，我不太想继续使用了
- **Hugo**：Go 编写的网站生成器

Go 的静态编译代表了工具的稳定性，因此我选择了 Hugo。而且 Hugo 的生态看起来也已经不错，showcase 中有些有名气的商业公司也在用它。但看了一眼它的配置，有一种堆叠了很多特性、缺乏设计的感觉。看日后的使用会不会受到困扰。

## 主题选择

事实上，对比用什么博客系统，我更关心有没有喜欢的主题。看到 @mdo 的 [网站][mdo-website] 及他做的 [poole][] 主题，我很喜欢。mdo 的网站是我喜欢的风格：首页把全部内容列出来，没有多余的排版和装饰。它是基于 poole 主题做的，但是做了很多优化，比如在亮色和暗色模式下都很漂亮的 syntax highlighting，比如代码块在移动设备下的滑动体验等等。可惜这些改动并没有开源，也没有 port 回 poole 主题中。因此我放弃了。

Hugo 的主题，主要相中 [PaperMod][] 及 [Terminal][]。Terminal 实在太有趣了，但问题是 typography 可能不够好，h1 ~ h6 似乎都一个大小，而且等宽字体的可读性不够好。PaperMod 比较简洁，中规中矩，觉得还可以，最终选择了它。

题外话：PaperMod 在 GitHub 有 2.7k 的 star，已经是 Hugo 主题中最高的了。但 Jekyll 在主题的 [丰富性][jekyll-themes] 上完爆 Hugo，有很多个高 star 主题。

[mdo-website]: https://markdotto.com/
[poole]: https://github.com/poole/poole
[PaperMod]: https://themes.gohugo.io/themes/hugo-papermod/
[Terminal]: https://themes.gohugo.io/themes/hugo-theme-terminal/
[jekyll-themes]: https://github.com/topics/jekyll-theme

## 内容发布

内容会主要发布在 [Twitter][my-twitter] 上。Twitter 让我容易触达跟我类似的人群。可能也会发一份到即刻或者豆瓣上。

[my-twitter]: https://twitter.com/onlyice0328

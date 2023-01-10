# Zhiheng's Blog

## Usage

1. 增加一个 Markdown 文件
2. `hugo server -D`

## Theme

主题用了 [PaperMod][]。使用 submodule 方法引入的主题：

```shell
git submodule add https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod --depth=1
```

clone 下博客时，需要运行命令来拉取 submodule：

```shell
git submodule update --init --recursive
```

可以这样更新主题：

```shell
git submodule update --remote --merge
```

[PaperMod]: https://adityatelange.github.io/hugo-PaperMod/

### Customize

为了定制一些样式，在 `config.yml` 中定义了 `customCSS`，通过 `layouts/partials/extend_head.html` 引入了它。`extend_head.html` 是 PaperMod 主题预留的 partial，供用户在 `<head>` 中加入自己的代码。
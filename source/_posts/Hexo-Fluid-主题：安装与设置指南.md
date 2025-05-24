---
title: Hexo Fluid 主题：安装与设置指南
tags:
  - hexo
  - 主题
  - fluid
categories:
  - 学习笔记
index_img: /img/fluid_logo.jpg
banner_img: 
banner_mask_alpha: 0.3
sticky: 
comments: 'valine'
date: 2025-05-24 09:25:00
---

## Hexo Fluid 主题：安装与设置指南

Fluid 是基于 Hexo 的一款 Material Design 风格的主题，由 Fluid-dev 开发与维护。本指南将基于您提供的资料，介绍如何安装和设置 Hexo Fluid 主题。

## 开始使用：安装主题

在开始之前，您需要先搭建好 Hexo 博客。如果您还没有 Hexo 博客，请按照 Hexo 官方文档进行安装和建站。

安装 Fluid 主题有两种主要方式：

### 方式一：通过 Npm 安装 (推荐，Hexo 5.0.0 及以上版本)

进入您的 Hexo 博客目录，执行以下命令：

```bash
npm install --save hexo-theme-fluid
```

然后在博客目录下创建 `_config.fluid.yml` 文件，并将主题目录下的 `_config.yml` 内容复制到新创建的 `_config.fluid.yml` 文件中。今后，所有主题配置的修改都建议在此文件中进行，以避免主题更新时丢失自定义配置。

### 方式二：下载 Release 压缩包安装

下载 Fluid 主题的最新 Release 版本。解压下载的压缩包到您 Hexo 博客目录下的 `themes` 文件夹。将解压出的文件夹重命名为 `fluid`。

**注意：** 如果您选择此方式安装主题，建议学习使用 **覆盖配置** 功能，避免在更新主题时丢失自定义配置。对于 Hexo 5.0.0 版本及以上的用户，可以在博客目录下创建 `_config.fluid.yml` 文件；对于 Hexo 低于 5.0.0 但不低于 3.0.0 的用户，需要在博客目录下的 `source/_data` 目录（如不存在则创建）中创建 `fluid_config.yml` 文件。将主题的 `_config.yml` 内容复制到这些文件中进行修改。

### 指定主题

修改 Hexo 博客目录下的 `_config.yml` 文件：

```yaml
theme: fluid # 指定主题
language: zh-CN # 指定语言，会影响主题显示的语言，按需修改
```

### 创建「关于页」

首次使用主题时，需要手动创建「关于页」。在博客目录下执行命令：

```bash
hexo new page about
```

创建成功后，修改 `/source/about/index.md` 文件，添加 `layout: about` 属性。修改后的文件示例如下：

```markdown
---
title: 标题
layout: about
---
这里写关于页的正文，支持 Markdown , HTML
```

**重要提示：** `layout: about` **必须存在，并且不能修改成其他值**，否则不会显示头像等样式。

## 配置主题

主题配置可以通过修改 `theme/fluid/_config.yml` 或站点目录下的 **主题配置文件** (`_config.fluid.yml` 或 `source/_data/fluid_config.yml`) 来实现。推荐使用后者的覆盖配置方式。本指南提到的“站点配置”指 Hexo 博客目录下的 `_config.yml`，“主题配置”指 `theme/fluid/_config.yml` 或 `_config.fluid.yml`。

几乎每个配置在主题配置文件中都有注释，可配合指南共同参考使用。

### 全局配置

*   **覆盖配置**: 如前所述，通过在站点根目录下创建 `_config.fluid.yml` (Hexo 5.0.0+) 或在 `source/_data/` 下创建 `fluid_config.yml` (Hexo < 5.0.0)，可以将主题配置放在主题文件夹之外，以便于更新。**只要存在于这些覆盖文件中的配置，优先级都高于主题自带的 `_config.yml`**。
*   **静态资源**: 可以通过主题配置中的 `static_prefix` 修改静态资源文件的 URL。
*   **本地搜索**: 已集成 `hexo-generator-search` 插件。默认生成并使用 `local-search.xml`。
*   **页面顶部大图 (Banner)**: 主题配置中，每个页面都有 `banner_img` 属性。可以使用本地图片相对路径（相对于 `source` 目录，优先使用博客目录下的 `source`）或外站链接。建议图片大小在 1MB 以内。可以使用 `banner_img_height` (0-100) 控制高度，`banner_mask_alpha` (0-1.0) 控制蒙版透明度。
    *   每篇文章可以单独设置 Banner，详见文章页设置。
    *   主题不支持固定背景 (fixed)。
*   **博客标题**: 页面左上角的标题默认使用 **站点配置** 中的 `title`。如需单独设置，可在 **主题配置** 中设置 `navbar.blog_title`。
*   **导航菜单**: 在 **主题配置** 的 `navbar.menu` 中设置。每个菜单项包含 `key` (用于语言关联，或直接显示值)、`link` (跳转链接)、`icon` (图标 CSS Class，可省略) 和 `name` (强制显示名称，可省略)。支持二级菜单。
*   **懒加载**: 默认开启。开启后，图片或评论插件在滚动到可见范围时才会加载，可提高网页打开速度。可在 **主题配置** 的 `lazyload` 项中设置是否启用 (`enable`)、加载占位图 (`loading_img`)、是否仅在文章页生效 (`onlypost`) 和触发加载的偏移倍数 (`offset_factor`)。
*   **全局字体**: 可在 **主题配置** 的 `font` 项中设置全局字号 (`font_size`)、字体族 (`font_family`) 和代码字号 (`code_font_size`)。建议使用系统自带字体，并至少添加一个通用字体族名。
*   **网页统计**: 支持多种统计服务，如百度统计、Google 统计、腾讯统计、51.la、友盟/cnzz、LeanCloud。在 **主题配置** 的 `web_analytics` 项中开启并填入相应的 Key 或 ID。
*   **PV 与 UV 统计**: 可在页脚展示。支持 LeanCloud 和 不蒜子。在 **主题配置** 的 `footer.statistics` 中设置是否启用 (`enable`)、数据源 (`source`) 和显示文本格式 (`pv_format`, `uv_format`)。
    *   不蒜子无需账号，但有时响应慢。LeanCloud 需要申请账号并填入 API 参数。
*   **语言配置**: 在 **站点配置** 的 `language` 项中设置。值需要对应主题 `languages/` 目录内的文件名。也可以通过在 `source/_data/languages` 目录下创建相应的 YAML 文件来自定义或新增语言配置。
*   **强制全局 HTTPS**: 在 **主题配置** 中开启 `force_https: true` 可将所有请求强制升级为 HTTPS。
*   **二级站点路径**: 如果博客部署在二级路径（如 `xxx.com/blog/`），需要修改 **站点配置** 中的 `url` 和 `root`。
*   **自定义 JS / CSS / HTML**: 可在 **主题配置** 的 `custom_js`, `custom_css`, `custom_head`, `custom_html` 项中引入自定义代码或文件。`custom_js` 和 `custom_css` 支持指定多个路径。
*   **暗色模式**: 在 **主题配置** 的 `dark_mode` 中开启 `enable: true`。`default` 参数可设置默认模式 (auto/light/dark)。
*   **OpenGraph**: 默认开启。可在 **主题配置** 的 `open_graph` 项中完善相关信息。也可在文章 front-matter 中设置 `og_img` 指定单页面的 OpenGraph 图片。

### 首页设置

*   **Slogan (打字机)**: 首页大图中的标题文字。可在 **主题配置** 的 `index.slogan` 中开启并设置文本。支持通过 API 获取内容。默认开启打字机动效，可在 `fun_features.typing` 中设置。
*   **文章摘要**: 可在 **主题配置** 的 `index.auto_excerpt` 中开启/关闭自动摘要 (默认开启)。手动指定摘要可通过在正文中使用 `<!-- more -->` 或在 front-matter 中设置 `excerpt` 字段。**优先级：手动摘要 > 自动摘要**。
*   **文章跳转方式**: 可在 **主题配置** 的 `index.post_url_target` 设置点击文章链接时的跳转方式 (`_blank` 新标签页, `_self` 当前标签页)。
*   **文章信息**: 可在 **主题配置** 的 `index.post_meta` 控制首页文章列表中是否显示发布时间、分类、标签。
*   **隐藏文章**: 在文章 front-matter 中设置 `hide: true` 可使文章不在首页及归档分类页中展示。隐藏后仍可通过链接访问。
*   **归档文章**: 在文章 front-matter 中设置 `archive: true` 可使文章在首页隐藏，但仍在归档分类页中展示。
*   **文章排序 (置顶)**: 如果安装了 `hexo-generator-index` >= 2.0.0 版本，可在文章 front-matter 中设置 `sticky` 属性。`sticky` 数值越大，文章越靠前。可通过 **主题配置** 的 `index.post_sticky` 控制是否显示置顶图标。

### 文章页设置

*   **文章在首页的封面图**: 在文章 front-matter 中设置 `index_img`。支持本地图片路径 (相对于 `source` 目录) 或外链。可在 **主题配置** 的 `post.default_index_img` 设置默认封面图。
*   **文章页顶部大图**: 默认显示主题配置中的 `post.banner_img`。可在文章 front-matter 中指定 `banner_img` 设置单篇文章的顶部大图。
*   **文章内容图片**: 本地图片存放位置（相对于 `source` 目录）同上。
*   **日期/字数/阅读时长/阅读数**: 显示在文章页大标题下方。可在 **主题配置** 的 `post.meta` 中开启/关闭作者 (`author`)、日期 (`date`)、字数统计 (`wordcount`)、阅读时间 (`min2read`) 和阅读次数 (`views`)。阅读次数支持 LeanCloud 或 不蒜子。日期格式需遵循 ISO-8601 规范。
*   **代码块**: 可在 **主题配置** 的 `code` 中设置是否开启复制按钮 (`copy_btn`)、行号 (`line_number`)、代码高亮 (`highlight`) 及选择高亮库 (`lib`，支持 highlightjs 和 prismjs)。
*   **评论**: 在 **主题配置** 的 `post.comments` 中开启 `enable: true` 并指定 `type`。下方需设置对应评论模块的参数。主题支持多种评论插件，如 Valine, Waline, Gitalk, Disqus 等。可在文章或自定义页面 front-matter 中设置 `comment: bool` 或 `comment: 'type'` 控制评论开关。
*   **脚注**: 主题内置脚注语法支持。可在 **主题配置** 的 `post.footnote` 中开启 (`enable: true`)。支持在文末生成带锚点的脚注。
*   **Tag 插件**: 主题内置多种 Tag 插件，如便签 (`{% note %}`), 行内标签 (`{% label %}`), 折叠块 (`{% fold %}`), 勾选框 (`{% cb %}`), 按钮 (`{% btn %}`) 和组图 (`{% gi %}`)。
*   **LaTeX 数学公式**: 手动开启。需在 **主题配置** 的 `post.math` 中开启 (`enable: true`)，可设置是否按需加载 (`specific`) 和选择引擎 (`engine`，支持 mathjax 或 katex)。同时需要更换 Markdown 渲染器（如 hexo-renderer-pandoc + Pandoc for mathjax, 或 hexo-renderer-markdown-it + @traptitech/markdown-it-katex for katex）。完成后需执行 `hexo clean`。
*   **Mermaid 流程图**: 手动开启。需在 **主题配置** 的 `post.mermaid` 中开启 (`enable: true`)，可设置是否按需加载 (`specific`) 和配置选项 (`options`)。支持内置 Tag 或代码块书写。

### 其他页面

*   **归档页/分类页/标签页**: 具体配置见主题配置文件注释。标签页支持词云展示。
*   **关于页**: 前面已介绍创建方法。可在 **主题配置** 的 `about` 项中设置关于信息 (头像 `avatar`, 姓名 `name`, 简介 `intro`) 和社交图标 (`icons`)。社交图标可设置链接或二维码。
*   **友情链接页**: 默认关闭。需先在 `navbar.menu` 中开启 `links` 菜单项，然后在 `links` 配置项中设置友情链接列表 (`items`)。支持自定义区域和评论。
*   **自定义页面**: 可通过 `hexo new page example` 创建。可在 front-matter 或 **主题配置** 的 `page` 项中进行配置。自定义页面评论通过 front-matter 控制。如果需要与文章页功能相似的自定义页面，建议使用 `_posts` 并配合隐藏文章功能。
*   **404 页**: 访问不存在的链接时显示。需要在部署环境上配置 (如 Nginx 的 `error_page 404`)。GitHub Pages 需绑定顶级域名才生效。主题包含默认 404 页面，也可在 `source` 目录下放置自定义的 `404.html`。

## 更新主题

根据您的安装方式，有不同的更新方法：

*   **Npm 安装**: 在博客目录下执行 `npm update --save hexo-theme-fluid`。
*   **Release 压缩包安装 (未修改代码)**: 将原文件夹重命名备份，重新下载最新 Release 并解压重命名为 `fluid`。根据更新说明同步修改您的覆盖配置文件 (`_config.fluid.yml` 或 `source/_data/fluid_config.yml`)。
*   **自定义代码或体验其他分支**: 确保 Fluid 目录开启 git 且所有改动已 commit。拉取对应分支的代码（如 dev 分支）：`git pull https://github.com/fluid-dev/hexo-theme-fluid.git develop`。解决代码冲突。

## 其他

*   **高级用法**: 主题提供了 Fluid 代码注入功能，相比 Hexo 内置注入器，支持注入 ejs 代码，更细致丰富。可在博客目录 `scripts` 文件夹下创建 JS 文件，使用 `hexo.extend.filter.register('theme_inject', ...)` 来实现。
*   **Hexo 插件**: 您提供的资料列出了一些推荐的 Hexo 插件，例如 `hexo-all-minifier` (压缩文件)、`hexo-abbrlink` (生成永久链接)、`live2d-widget` (看板娘) 等。**请注意，所有插件仅作为推荐，不能保证完全与 Fluid 兼容，请仔细阅读插件文档**。
*   **加快网页加载**: 推荐使用 OSS (对象存储服务) 托管博客静态文件。对于本地图片，建议搭配 `hexo-all-minifier` 插件进行压缩；对于外部图片，建议使用 tinypng 等工具压缩。

**提示**: 每次无论是 `hexo g` (生成) 或 `hexo s` (本地服务)，都最好先使用 `hexo clean` 清除本地缓存，以避免奇怪的问题。

希望这篇指南能帮助您更好地安装和设置 Hexo Fluid 主题！

```

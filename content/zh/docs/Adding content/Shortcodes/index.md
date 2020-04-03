---
title: "Docsy简码"
linkTitle: "Docsy简码"
date: 2017-01-05
weight: 5
description: >
  使用Docsy雨果简码快速构建网站的网页。
resources:
  - src: "**spruce*.jpg"
    params:
      byline: "Photo: Bjørn Erik Pedersen / CC-BY-SA"
---

Rather than writing all your site pages from scratch, Hugo lets you define and use [shortcodes](https://gohugo.io/content-management/shortcodes/). These are reusable snippets of content that you can include in your pages, often using HTML to create effects that are difficult or impossible to do in simple Markdown. Shortcodes can also have parameters that let you, for example, add your own text to a fancy shortcode text box. As well as Hugo's [built-in shortcodes](https://gohugo.io/content-management/shortcodes/), Docsy provides some shortcodes of its own to help you build your pages.

## 简码块

The theme comes with a set of custom **Page Block** shortcodes that can be used to compose landing pages, about pages, and similar.

These blocks share some common parameters:

height
: A pre-defined height of the block container. One of `min`, `med`, `max`, `full`, or `auto`. Setting it to `full` will fill the Viewport Height, which can be useful for landing pages.

color
: The block will be assigned a color from the theme palette if not provided, but you can set your own if needed. You can use all of Bootstrap's color names, theme color names or a grayscale shade. Some examples would be `primary`, `white`, `dark`, `warning`, `light`, `success`, `300`, `blue`, `orange`. This will become the **background color** of the block, but text colors will adapt to get proper contrast.

### blocks/cover

**blocks/cover** 短代码创建填充页面的顶部块的着陆页类型。

```html
{{</* blocks/cover title="Welcome!" image_anchor="center" height="full" color="primary" */>}}
<div class="mx-auto">
	<a class="btn btn-lg btn-primary mr-3 mb-4" href="{{</* relref "/docs" */>}}">
		Learn More <i class="fas fa-arrow-alt-circle-right ml-2"></i>
	</a>
	<a class="btn btn-lg btn-secondary mr-3 mb-4" href="https://example.org">
		Download <i class="fab fa-github ml-2 "></i>
	</a>
	<p class="lead mt-5">This program is now available in <a href="#">AppStore!</a></p>
	<div class="mx-auto mt-5">
		{{</* blocks/link-down color="info" */>}}
	</div>
</div>
{{</* /blocks/cover */>}}
```

需要注意的是相关的简码参数上面会有合理的默认值，但此处是出于完整性包括在内。

{{% alert title="Hugo Tip" %}}

> 使用支架风格的简码的分隔符, `>}}`, 告诉`Hugo`内部的内容是 HTML/纯文本并且不需要进一步的处理.
> 更改分隔符`％}}` 意味着 `Hugo`将把内容作为'Markdown`.
> 您可以在页面中使用这两种风格。

{{% /alert %}}

| 参数         | 默认                 | 描述                 |
| ------------ | -------------------- | -------------------- |
| title        |                      | 主显示标题用于该块。 |
| image_anchor |                      |                      |
| height       |                      | 看上面。             |
| color        |                      | 看上面。             |
| byline       | 特色图片上署名文字。 |                      |

要设置背景图片, place an image with the word "background" in the name in the page's [Page Bundle](/docs/adding-content/content/#page-bundles).
For example, in our the example site the background image in the home page's cover block is [`featured-background.jpg`](https://github.com/google/docsy-example/tree/master/content/en), in the same directory.

{{% alert title="Tip" %}}
If you also include the word **featured** in the image name, e.g. `my-featured-background.jpg`, it will also be used as the Twitter Card image when shared.
{{% /alert %}}

有关可用图标, 查看 [Font Awesome](https://fontawesome.com/icons?d=gallery&m=free).

### blocks/lead

**blocks/lead** 块短码是与居中的文本和向下指向下一个部分的箭头一个简单的铅/标题块。

```go-html-template
{{%/* blocks/lead color="dark" */%}}
TechOS is the OS of the future.

Runs on **bare metal** in the **cloud**!
{{%/* /blocks/lead */%}}
```

| Parameter | Default | Description |
| --------- | ------- | ----------- |
| height    |         | See above.  |
| color     |         | See above.  |

### blocks/section

**blocks/section** 短码是指作为一个通用的内容容器。

它有两个“`flavors`”, 一个普通的内容 和 一个与样式更适合于包装的特征部分的水平行.

下面示出了部分包裹 3 个特征部分的实施例。

```go-html-template
{{</* blocks/section color="dark" */>}}
{{%/* blocks/feature icon="fa-lightbulb" title="Fastest OS **on the planet**!" */%}}
The new **TechOS** operating system is an open source project. It is a new project, but with grand ambitions.
Please follow this space for updates!
{{%/* /blocks/feature */%}}
{{%/* blocks/feature icon="fab fa-github" title="Contributions welcome!" url="https://github.com/gohugoio/hugo" */%}}
We do a [Pull Request](https://github.com/gohugoio/hugo/pulls) contributions workflow on **GitHub**. New users are always welcome!
{{%/* /blocks/feature */%}}
{{%/* blocks/feature icon="fab fa-twitter" title="Follow us on Twitter!" url="https://twitter.com/GoHugoIO" */%}}
For announcement of latest features etc.
{{%/* /blocks/feature */%}}
{{</* /blocks/section */>}}
```

| 参数   | 默认 | 描述                                                                                   |
| ------ | ---- | -------------------------------------------------------------------------------------- |
| height |      | See above.                                                                             |
| color  |      | See above.                                                                             |
| type   |      | 指定“`section`”如果你想有一个一般的容器, 省略该参数，如果你想这个部分包含的功能水平行. |

### blocks/feature

```go-html-template

{{%/* blocks/feature icon="fab fa-github" title="Contributions welcome!" url="https://github.com/gohugoio/hugo" */%}}
We do a [Pull Request](https://github.com/gohugoio/hugo/pulls) contributions workflow on **GitHub**. New users are always welcome!
{{%/* /blocks/feature */%}}

```

| Parameter | Default | Description            |
| --------- | ------- | ---------------------- |
| title     |         | The title to use.      |
| url       |         | The URL to link to.    |
| icon      |         | The icon class to use. |

### blocks/link-down

**blocks/link-down** 简码创建的导航链接到下一个章节.
它意味着在组合使用与其它块简码。

```go-html-template

<div class="mx-auto mt-5">
	{{</* blocks/link-down color="info" */>}}
</div>
```

| Parameter | Default | Description |
| --------- | ------- | ----------- |
| color     | info    | See above.  |

## 简码助手

### alert

**alert** 短码产生了可以用来显示通知或警告警报块.

```go-html-template
{{%/* alert title="Warning" color="warning" */%}}
This is a warning.
{{%/* /alert */%}}

```

要呈现:

{{% alert title="Warning" color="warning" %}}
This is a warning.
{{% /alert %}}

| Parameter | Default | Description                                                   |
| --------- | ------- | ------------------------------------------------------------- |
| color     | primary | One of the theme colors, eg `primary`, `info`, `warning` etc. |

### pageinfo

**pageinfo** 简码创建一个文本框，您可以使用添加旗帜信息页面: 例如，让用户知道该页面包含占位符的内容，该内容已过时，或者说，它记录了一个测试版功能.

```go-html-template
{{%/* pageinfo color="primary" */%}}
This is placeholder content.
{{%/* /pageinfo */%}}

```

要呈现:

{{% pageinfo color="primary" %}}
This is placeholder content
{{% /pageinfo %}}

| Parameter | Default | Description                                                   |
| --------- | ------- | ------------------------------------------------------------- |
| color     | primary | One of the theme colors, eg `primary`, `info`, `warning` etc. |

### imgproc

**imgproc** 短码找到在当前[Page Bundle](/docs/adding-content/content/#page-bundles)和体重秤它给定一组处理指令的图像。

```go-html-template
{{</* imgproc spruce Fill "400x450" */>}}
Norway Spruce Picea abies shoot with foliage buds.
{{</* /imgproc */>}}
```

{{< imgproc spruce Fill "400x450" >}}
Norway Spruce Picea abies shoot with foliage buds.
{{< /imgproc >}}

上面的例子有还具有添加照片归因署名。
当使用插图从[维基](https://commons.wikimedia.org/)免费许可和类似, 你会在大多数情况下，需要一种方法来属性作者或许可。
您可以在页面前面的问题元数据添加到您的网页资源。
该`byline`参数是在这个主题中使用的约定:

```yaml
resources:
  - src: "**spruce*.jpg"
    params:
      byline: "Photo: Bjørn Erik Pedersen / CC-BY-SA"
```

| 参数 | 描述                                                                                                                                        |
| ---: | ------------------------------------------------------------------------------------------------------------------------------------------- |
|    1 | 图像文件名或足够的它，以确定它（我们做的水珠匹配）                                                                                          |
|    2 | 命令. 之一 `Fit`, `Resize` 要么 `Fill`. 看 [图像处理方法](https://gohugo.io/content-management/image-processing/#image-processing-methods). |
|    3 | 处理选项, 如 `400x450`. 看 [影像处理选项](https://gohugo.io/content-management/image-processing/#image-processing-methods).                 |

### swaggerui

`swaggerui` 短代码可以放在[`swagger`](https://github.com/google/docsy/tree/master/layouts/swagger)布局的页面内任何地方 ;
它呈现使用任何的 OpenAPI YAML 或 JSON 文件作为源[Swagger UI](https://swagger.io/tools/swagger-ui/)。
这可以在任何地方托管你喜欢, 例如，在网站根目录 [`/static` 文件夹](/docs/adding-content/content/#adding-static-content).

```yaml
---
title: "Pet Store API"
type: swagger
weight: 1
description: Reference for the Pet Store API
---
{ { </* swaggerui src="/openapi/petstore.yaml" */> } }
```

您可以自定义 Swagger UI 外观 and feel by overriding Swagger's CSS or by editing and compiling a [Swagger UI dist](https://github.com/swagger-api/swagger-ui) yourself and replace `themes/docsy/static/css/swagger-ui.css`.

---
title: "文档版本"
date: 2020-02-02
weight: 4
description: >
  自定义导航和您的文档的多个版本的横幅。
---

根据项目的发布和版本，您可能希望让用户访问您的文件的以前版本。
你如何部署以前的版本是由你。
本页介绍 Docsy 功能，您可以使用您的文档的不同版本之间提供导航，并显示在存档网站的信息旗帜。

## 添加一个版本下拉菜单

If you add some `[params.versions]` in `config.toml`, the Docsy theme adds a
version selector drop down to the top-level menu. You specify a URL and a name
for each version you would like to add to the menu, as in the following example:

```
# Add your release versions here
[[params.versions]]
  version = "master"
  url = "https://master.kubeflow.org"

[[params.versions]]
  version = "v0.2"
  url = "https://v0-2.kubeflow.org"

[[params.versions]]
  version = "v0.3"
  url = "https://v0-3.kubeflow.org"
```

Remember to add your current version so that users can navigate back!

The default title for the version drop-down menu is **Releases**. To change the
title, change the `version_menu` parameter in `config.toml`:

```
version_menu = "Releases"
```

You can read more about Docsy menus in the guide to
[navigation and search](/docs/adding-content/navigation/).

## 展示一个横幅上进行归档的文档网站

If you create archived snapshots for older versions of your docs, you can add a
note at the top of every page in the archived docs to let readers know that
they’re seeing an unmaintained snapshot and give them a link to the latest
version.

For example, see the archived docs for
[Kubeflow v0.6](https://v0-6.kubeflow.org/docs/):

<figure>
  <img src="/images/version-banner.png"
       alt="A text box explaining that this is an unmaintained snapshot of the docs."
       class="mt-3 mb-3 border border-info rounded" />
  <figcaption>Figure 1. The banner on the archived docs for Kubeflow v0.6
  </figcaption>
</figure>

To add the banner to your doc site, make the following changes in your
`config.toml` file:

1. Set the `archived_version` parameter to `true`:

   ```
   archived_version = true
   ```

1. Set the `version` parameter to the version of the archived doc set. For
   example, if the archived docs are for version 0.1:

   ```
   version = "0.1"
   ```

1. Make sure that `url_latest_version` contains the URL of the website that you
   want to point readers to. In most cases, this should be the URL of the latest
   version of your docs:

   ```
   url_latest_version = "https://your-latest-doc-site.com"
   ```

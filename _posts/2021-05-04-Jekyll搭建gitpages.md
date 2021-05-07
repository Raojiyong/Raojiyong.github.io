---
title: Jekyll搭建Gitpages
author: Jiyong Rao
date: 2021-05-04 21:20:30 +0800
categories: ["2021", "05"]
tags: [tutorial]
---

## GitPages + Jekyll

我使用的是[Jekyll-theme-chirpy](https://github.com/cotes2020/chirpy-starter)模板，直接拿来。因为有Git的基础，用起来还是比较方便的。另外，gitpages本身的主题比较少而且不是很好看，所以用了第三方的，第三方还是很多的。

这个模板需要注意的就是，要另外创建新branch，注意`./github/workflows/pages-deply.yml、tools/deploy.sh`文件的branch名，还有基础配置文件`_config.yml`的更改。

### Markdown基础

在写blog的时候，也学了一点markdown基础。

这是**加粗**，*斜体*，链接[百度](https://baidu.com)，复选框

- [x] 复选

插入代码`int x`，插入代码块

``````sdadknsadan
for(int x;x<n;x++){
	printf("%d",x);
}
``````

插入图片

![小火箭](./4.png)

- 一
- 二
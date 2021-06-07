---
title: hexo themes 下提交不到github
date: 2021-06-07 19:15:17
tags: hexo
categories: hexo
---

## 原因
因为`themes/light`也是从仓库里拉取下来的 他关联到了作者的`git`仓库 所以提交不上去

## 处理

从暂存区删除该文件夹
    bash git rm --cache themes/主题文件名  
---
title: JavaScript 学习
date: 2021-06-01 23:36:51
tags: 
- JavaScript
- vscode
categories: JavaScript
---
## 使用 vscode 
学习的几个 vscode 设置

1. 如何运行js代码 ？
    
    新建js脚本，使用 `run` 插件即可(其实是运行的nodejs代码)  
    + 如果要测试浏览器脚本，还是需要浏览器的配合  
    推荐插件 `live Server` 实时预览html界面  
    ![live Server](https://ritwickdey.gallerycdn.vsassets.io/extensions/ritwickdey/liveserver/5.6.1/1555497731217/Microsoft.VisualStudio.Services.Icons.Default) [![VSCode Marketplace](https://img.shields.io/vscode-marketplace/v/ritwickdey.LiveServer.svg?style=flat-square&label=vscode%20marketplace)](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)  

    + 如果需要调试就需要安装 debugger for edge/chrome/firefox etc.

2. vscode 设置
    在使用推荐模板在之后，在模板内输入自动提示就消失了

        "editor.quickSuggestions": true
        "editor.suggest.snippetsPreventQuickSuggestions": false
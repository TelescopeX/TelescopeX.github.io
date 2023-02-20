
---
title: 如何更换Hexo主题
---

## 一，下载存放主题：
第一步：到hexo官网下载hexo主题包（压缩包一般存储在GitHub上）。

  1. 把压缩包解压到博客系统的文件夹themes。（我的是 E:/blog/themes）

## 第二步：使用node更换主题
  2. 使用nond控制栏工具，进入到我们Hexo的安装包下面。我的hexo主题放在E盘的blog中。因此，我输入下述代码

$ E： （先是进入E盘）
$ cd blog  （再进入blog）

## 第三步：修改blog文件下_config.yml文件内容。
  3. 在我们hexo安装包中找到_config.yml安装包，用编译器打开（vscode或者sublime）。
command + F 查找 theme将原来默认的主题 landscape 改为 下载的文件夹名称（hexo-theme-nexmoe-master）。修改好的代码参考以下：

## theme: hexo-theme-nexmoe-master

## 第四步：预览效果！
接下来，我们先来预览一下，我们主题更换的效果

$ hexo s  （重启服务器）

复制浏览器打开生成的链接就可以看到效果了！
到这一步，我们基本上上完成了，主题的更换。

最后，
总结

纸上得来终觉浅，绝知此事要躬行！
多敲代码，多动脑子！


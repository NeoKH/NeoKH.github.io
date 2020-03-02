---
title: VSCode插件之PicGo
tags:
  - VSCode

---



# VSCode插件之PicGo



`PicGo`是一个**图床管理工具**，支持微博、七牛云、腾讯云COS、又拍云、GitHub、阿里云OSS、SM.MS、imgur 等8种常用图床，简单易用。目前最新版本是2.0。因为直接安装`PicGo`需要`Node.js`，我不想再安装`Node.js`，于是选择使用`VSCode`的`PicGo`插件。

## 设置

###  step1   选择你的图床平台。

我选择的图床是github仓库。之前用过微博图床和聚合图床。微博图床使用的是Chrome的插件，但好像不再维护，界面老旧，于是没有再用。聚合图床一开始很好用，但一天下午突然崩了。最终还是选择迁到github。

在github中新建一个仓库就可以作为图床了。

### step2  获取token

建好仓库后，需要获取token。

依次点击`头像`==>`setting`==>`Developer settings`==>`personal access tokens`==>`generate new token`.

![图片不存在哦](..\assets\image\2020-03-02-1.JPG)

在`note`中填写该`token`的用途，并勾选下方`repo`选项，然后点击`generate token`即可。

注意生成的token只会出现一次，所以要把token保存到其他地方，以免遗忘。并且应注意保密。token相当于操作你github仓库的通行证，有了这个通信证，别人就可以不经允许上传文件甚至修改删除文件。

### step3  设置PicGo插件

在VSCode中安装PicGo插件，安装完成后，打开`extension setting`，如下：

![图片不存在哦](..\assets\image\2020-03-02-2.jpg)

在`current`中选择`github`，分支选择主分支，在Repo中填写`用户名/仓库名`，在`path`中填写你希望图片保存的路径，例如我写的是`others/`，那么图片会保存在`imagebed/others/`路径下。实际使用中，`Path`可以经常改动以将图片保存在不同位置。最后填入生成的`token`。至此，配置完毕。



## 使用方法

支持三种上传图片的方式。打开`.md`或`.html`文档（仅支持这两种文档），在你想插入图片的位置按下述快捷键：

- 从剪切板上传: `Ctrl + Alt + U`

  <img src="..\assets\image\2020-03-02-3.gif" style="zoom:50%;" />

- 从文件夹上传: `Ctrl + Alt + E`

  <img src="..\assets\image\2020-03-02-4.gif" style="zoom:50%;" />

- 输入图片名上传: `Ctrl + Alt + O`

  <img src="..\assets\image\2020-03-02-5.gif" style="zoom:50%;" />



参考：

- [官方文档](https://picgo.github.io/PicGo-Doc/zh/guide/)

- [开发者博客](https://sspai.com/post/52527)

- [动图来源](https://wangdaodao.com/20190208/vscode-picgo.html)

  




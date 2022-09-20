[TOC]

## 【经验分享】关于RT-Thread studio gitee源下载软件包失败以及git拉取Gitee仓库报错

#### 问题描述

> 最近在RT-Thread Studio上进行项目开发时突然遇到以前没有遇到过的问题：软件包下载不成功。
> 由于我最开始使用的是gitee源下载，所以我更换成github源下载，结果也是不成功，考虑到国内对于GitHub的访问需要用到梯子，所以在开启之后发现还是下载不成功。
> 不死心的我打算直接从Gitee上直接拉取资源包，结果发现git也无法使用了，最后所幸找到了解决办法。

#### 分析
>由于一般在开发过程中有使用梯子的需要，所以可能是某次不知情操作下更改了Git的下载方式，导致Git拉取使用代理。

#### 解决办法
> 首先查看Git是否使用了代理

```c
git config --global http.proxy
```
>如果使用了代理的话，回车会显示代理地址，没有的话就不会显示

>然后我们取消代理
```c
git config --global --unset http.proxy
```

> 此时我们再重启RT-Thread studio更新软件包就可以发现gitee源成功下载，Git也同样能够正常使用了！

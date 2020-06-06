---
layout: post
title:  PicGo+GitHub图床
date:   2019-12-09
categories: Tools
tags: PicGo GitHub图床
---
* content
{:toc} 






先来一张照片 ！ 哈哈哈
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0hvbmdHSHUvdHVjaHVhbmcvbWFzdGVyLzQwM2E0Y2NmZ3kxZzc5aGs1dzlwOWoyMHUwMWhjazVzLmpwZw?x-oss-process=image/format,png)

## [typora](https://www.typora.io/)

官网：<https://www.typora.io/>
## [PicGo介绍](https://github.com/Molunerfinn/PicGo/releases)

github:<https://github.com/Molunerfinn/PicGo/releases>

这是一款图片上传的工具，目前支持微博图床，七牛图床，腾讯云，又拍云，GitHub等图床，未来将支持更多图床。

所以解决问题的思路就是，将本地的文件，或者剪切板上面的截图发送图床，然后生成在线图片的链接，这样就可以让Markdown文档飞起来了，走到哪就可以用到哪     

## 创建自己的GitHub图床    
### 1. 创建GitHub图床之前，需要注册/登陆GitHub账号
### 2. 创建Repository
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191204163557963.png)
###  3.生成一个Token用于操作GitHub repository    
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191204163757729.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0hIRzIwMTcxMjI2,size_16,color_FFFFFF,t_70)
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191204163826412.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0hIRzIwMTcxMjI2,size_16,color_FFFFFF,t_70)
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191204163842962.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0hIRzIwMTcxMjI2,size_16,color_FFFFFF,t_70)
## 配置PicGo
### 1. 下载运行PicGo  
<https://github.com/Molunerfinn/PicGo/releases>   

### 2. 配置图床
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191204164001894.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0hIRzIwMTcxMjI2,size_16,color_FFFFFF,t_70)
 >- 设定仓库名的时候，是按照“账户名/仓库名的格式填写”
 >-  分支名统一填写“master”
 >- 将之前的Token黏贴在这里
 >- 存储的路径可以按照我这样子写，就会在repository下创建一个“img”文件夹
 >- 自定义域名的作用是，在上传图片后成功后，PicGo会将“自定义域名+上传的图片名”生成的访问链接，放到剪切板上https://raw.githubusercontent.com/用户名/RepositoryName/分支名，，自定义域名需要按照这样去填写      

### 3.快捷键及相关配置  
 ![在这里插入图片描述](https://img-blog.csdnimg.cn/20191204164138167.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0hIRzIwMTcxMjI2,size_16,color_FFFFFF,t_70)
-------------------------------------------------分割线-------------------------------------------------
![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9yYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tL0hvbmdHSHUvdHVjaHVhbmcvbWFzdGVyL3RpbWcuZ2lm)

自己又是 用 Typora 的时候，图片有时候加载不出来，可能是网速的问题                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          

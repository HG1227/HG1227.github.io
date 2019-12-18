---
layout: page
title: Collections
permalink: /collection/
icon: bookmark
type: page
---

* content
{:toc}

## 🚀 工具

- [Cmd Markdown 简明语法手册](https://www.zybuluo.com/mdeditor?url=https%3A%2F%2Fwww.zybuluo.com%2Fstatic%2Feditor%2Fmd-help.markdown#12)
- [tiny png](https://tinypng.com/)         用于压缩 png 或 jpg 的在线工具
- [icon image 网站](https://hg1227.github.io/2019/12/07/整理的一些工具/)

* [图床 https://sm.ms/](https://sm.ms/)

    有 API 可用。

* [Unix 时间戳 Unix timestamp](http://tool.chinaz.com/Tools/unixtime.aspx)

- [在线正则表达式匹配](https://regex101.com/)
    - 这个功能更强大一点，能清楚的区分出贪婪和懒惰正则。(原博客的)
- [http://regexr.com/](http://regexr.com/)
- [google fonts](https://fonts.google.com/)
  - [Google Fonts 加速代理](https://fengmk2.com/blog/2016/google-fonts-mirror)
- 菜单图标示例 : 1. [Font Awesome](https://www.bootcss.com/p/font-awesome/) 2. [Font Awesome](http://www.fontawesome.cn/)
- [Font Awesome](https://fontawesome.com/)  图标库 (自己还不会配置 )

## 编程语言

## 框架&脚手架



## 类库与插件



## 模块化



## other articles



## 编辑器



## GitBook 及其插件

* [Gitbook 的使用和常用插件 -赵达](http://zhaoda.net/2015/11/09/gitbook-plugins/)
* [gitbook-plugin-expandable-chapters](https://plugins.gitbook.com/plugin/expandable-chapters)

    折叠左侧目录章节。

    <!-- ![](http://ww4.sinaimg.cn/large/7011d6cfjw1f08kmplbj1j20gn05l0tk.jpg) -->

## Chrome 插件
- [Octotree](https://chrome.google.com/webstore/detail/octotree/bkhaagjahfmjljalopjnoealnfndnagc)

    - Code tree for GitHub and GitLab

* [Chrome扩展及应用开发 -图灵电子书](http://www.ituring.com.cn/minibook/950)

* [有哪些鲜为人知却非常有意思、好用的 Chrome 扩展？ -知乎](https://www.zhihu.com/question/23228162#answer-28057391)
* [Dribbble New Tab](https://chrome.google.com/webstore/detail/dribbble-new-tab/hmhjbefkpednjogghoibpejdmemkinbn)

    新建 tab 时，显示 dribbble 上的精选作品。

## Other blogs

[刘建平Pinard](https://www.cnblogs.com/pinard/)  \| [JerryLead](https://www.cnblogs.com/jerrylead/) 





| 名称          | 描述                                                         |
| ------------- | ------------------------------------------------------------ |
| container     | 用于渲染的容器，一般使用一个 div 即可                        |
| renderer      | 渲染器，可以选择 'svg' / 'canvas' / 'html'，个人测试发现 svg 效果和兼容性最好 |
| name          | 动画名称，用于 reference                                     |
| loop          | 循环                                                         |
| autoplay      | 自动播放                                                     |
| path          | json 路径，页面会通过一个 http 请求获取 json                 |
| animationData | json 动画数据，与 path 互斥，建议使用 path，因为 animationData 会将数据打包进来，会使得 js bundle 过大 |
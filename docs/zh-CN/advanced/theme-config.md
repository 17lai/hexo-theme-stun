# 主题配置

::: tip
修改配置文件，安装新的依赖等，都需要重启 hexo 服务器。
:::

## 配置文件

首先，你需要分清下面这两个配置文件的作用：

- hexo 根目录下的 `_config.yml`。这是站点配置文件，里面的配置作用于整个网站。
- stun 根目录下的 `_config.yml`。这是主题配置文件，里面的配置只对当前主题生效。

## 保留主题配置数据

如果你不想每次升级主题时，都要进行如下重复的操作：先将主题配置文件复制一份，等主题升级后再复制回去。那么你可以进行以下操作：将主题配置文件复制到 hexo 根目录下的 `source/_data/stun.yml` 文件中（没有此目录和文件就新建。目录名称不能改变，文件名称可以是任意的）。

> 如果你进行了上述操作，当你需要修改主题配置时，只需要修改 `stun.yml` 文件即可。更新主题时，主题根目录下的 `_config.yml` 文件（可能）会更新，而你对主题配置的数据仍保留在 `stun.yml` 文件中。

::: warning
注意，主题 `_config.yml` 文件中包含的配置项，在 `stun.yml` 文件中都要有。也就是说，上面这种做法虽然方便你保留主题的配置数据，但是当主题 `_config.yml` 文件的配置项更改时，如果你不及时手动更新 `stun.yml` 文件，主题很可能会报错。
:::

## 国际化（i18n）

修改**站点**配置文件（不是主题配置文件）：

``` yaml
language: zh-CN # 可选值 zh-CN 或 en-US
```

语言文件在主题文件夹的 languages 目录下。stun 主题默认有 `zh-CN.yml` 和 `en.yml` 两种语言文件，如果需要支持其他语言，请自行编写语言文件。语言文件的命名规则要求符合 [RFC 4646](http://www.ietf.org/rfc/rfc4646.txt) 标准，你可以在[这里](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry)找到各种语言的缩写。

## 顶部菜单栏

网站顶部菜单栏默认有 `/` 和 `/archives` 两个路径，它们分别对应于网站首页和归档页。如果你想添加：`categories`、`tags`、`about` 页面，你需要进行以下操作：

- 添加路径

修改 `stun.yml` 文件：

``` yaml
menu:
  home: /
  archives: /archives/
  categories: /categories/
  tags: /tags/
  about: /about/
```

- 添加图标

修改 `stun.yml` 文件：

``` yaml
menu:
  home: / || home
  archives: /archives/ || folder-open
  categories: /categories/ || th
  tags: /tags/ || tags
  about: /about/ || user
```

在路径后面添加 `||` 分隔符，然后添加你想要显示的图标名称。图标名称在这里获取：[https://fontawesome.com/v4.7.0/icons/](https://fontawesome.com/v4.7.0/icons/)

> 如果只添加路径，没有添加图标名称，会使用默认图标进行显示。

你可以通过修改 `menu_settings` 配置项来控制菜单项的图标是否显示：

``` yml
menu_settings:
  icon: true # true 表示显示，false 表示隐藏
```

- 新建页面

在 hexo 根目录执行指令：

``` bash
hexo new page xxx # xxx 表示页面名称
```

执行这条指令后，会在如下目录生成文件：`source/xxx/index.md`

::: warning
新建的页面名称，需要和 `stun.yml` 文件中添加的页面路径名称保持一致。

e.g. 你在 `stun.yml` 中设置了如下路径：
``` yaml
menu:
  about: /about-me
```

那么你应该执行指令：`hexo new page about-me`，这样才能在访问该路径时，找到对应的文件。
:::

## 自定义页面

如果你想在网站顶部菜单栏中添加自定义页面，请进行以下操作：

- 添加路径
- 添加图标
- 执行指令，新建页面

这三步的步骤同上。

- 国际化设置

找到 languages 目录下的语言文件进行修改。例如，自定义页面名称为 `read`，修改如下：

`zh-CN.yml`

``` yaml
nav:
  read: 阅读
```

`en.yml`

``` yaml
nav:
  read: Read
```

## Favicon

设置网站图标（favicon），修改 `stun.yml` 文件：

``` yaml
favicon:
  small: /imgs/favicon-16x16-stun.png
  medium: /imgs/favicon-32x32-stun.png
  # apple_touch_icon: /imgs/apple-touch-icon-stun.png
  # safari_pinned_tab: /imgs/logo-stun.svg
```

## 网站顶部信息

修改 `stun.yml` 文件：

``` yml
header:
  # 网站顶部的高度（设置为百分数，表示所占屏幕高度的百分比。支持所有 CSS 长度单位）
  height: 80%
  # 顶部导航栏的高度 (支持所有 CSS 长度单位)
  nav_height: 50px
  # 顶部背景图片
  bg_image:
    enable: true
    # 填写图片路径或链接
    url: 
  # 模糊滤镜效果（对网站顶部图片进行模糊）
  blur_effect:
    enable: false
    # 模糊程度
    level: 15px
```

## 页面、文章单独的顶部图

如果想要为某个页面或某篇文章单独指定顶部图，在页面或文章 `md` 源文件的 [front-matter](https://hexo.io/zh-cn/docs/front-matter) 中，添加 `top_image` 项，填入你想要的图片 url 或路径即可。例如：

``` yaml
---
title: Hello Stun
date: 2019-05-15 22:54:49
top_image: https://xxxx.jpg
tags:
  - hexo-theme
  - stun
---
```

## 知识共享许可协议

修改 `stun.yml` 文件：

``` yml
creative_commons:
  enable: true
  # 可选值: BY | BY-SA | BY-ND | BY-NC | BY-NC-SA | BY-NC-ND
  # 详情请访问: https://creativecommons.org/share-your-work/licensing-types-examples
  license: BY-NC-SA
  # 在侧边栏显示
  sidebar: true
  # 在文章底部显示许可协议
  post: true
  # 设置许可协议的显示语言（当用户点击查看许可协议时，会以你设置的语言进行显示）
  language: zh # zh 或 en 等等
```

## 返回顶部

修改 `stun.yml` 文件：

``` yml
back2top:
  enable: true
  icon:
    # 建议使用名为 `rocket` 的图标
    # 图标名称在这里查找：https://fontawesome.com/v4.7.0/icons/
    name: rocket
    # 火箭发射动画
    animation: true
    # 图标的旋转角度
    rotate: -45deg
    # 支持使用所有的 CSS 颜色单位
    color: "#49b1f5"
    hover_color: "#fc6423"
```

## 网站底部信息

修改 `stun.yml` 文件：

``` yml
footer:
  # 顶部背景图
  bg_image:
    enable: true
    # 填写图片路径或链接
    url: 
  # 版权信息
  copyright:
    enable: true
    # 显示的文字信息，例如：xxx All Rights Reserved.
    # 如果不设置，将显示 hexo 配置文件中的 author 字段的内容
    text: 
    # 开始时间（如果不设置，将显示最新的年份）
    since: 
    # 结束时间（如果不设置，将显示最新的年份）
    end: 
  # 时间和文字信息之间的图标
  icon:
    enable: true
    # 建议使用名为 `heart` 的图标
    # 图标名称在这里查找：https://fontawesome.com/v4.7.0/icons/
    name: heart
    # 心跳动画
    animation: true
    # 请使用引号包裹颜色值（支持所有 CSS 颜色单位）
    color: "#ff0000"
  # Hexo 链接 (Powered by Hexo).
  powered:
    enable: true
    # 显示版本号 (例如：vX.X.X).
    version: true
  # 主题链接 (Theme - stun).
  theme:
    enable: true
    # 显示版本号 (例如：vX.X.X).
    version: true
  # 备案信息（只有中国开发者会用到）详情: http://www.miitbeian.gov.cn
  beian:
    enable: false
    # 备案 XXXXXXXX 号
    icp: 
  # 任何自定义文本，支持 HTML (例如：托管于 <a href="https://pages.github.com/" rel="noopener" target="_blank">Github Pages</a>).
  custom:
    enable: true
    text: 
```

## 侧边栏

``` yml
sidebar:
  enable: true
  # 侧边栏位置，可选值有：left 或 right
  float: right
  # 侧边栏距离顶部的距离（只支持 px 单位）
  offsetTop: 20px
  # 侧边栏的宽度（建议：260px ~ 360px，支持所有 CSS 长度单位）
  width: 300px
  # 是否显示水平分割线
  horizon_line: true
```

## 侧边栏头像

``` yml
author:
  enable: true
  # 侧边栏头像
  avatar:
    # 填写图片路径或链接
    url: 
    # 是否显示为圆形
    rounded: true
    # 头像透明度（取值：0 ~ 1）
    opacity: 1
    # 鼠标 hover 动画，可选值：trun 或 shake
    animation: shake

  # 格言（也可以是任意一句想写的话）
  motto: 
```

## 友链

``` yml
# `||` 分隔符前面表示友链的链接或信息，后面表示友链图标。
# 图标的名称在这里查找：https://fontawesome.com/v4.7.0/icons/
# 如果你找不到想要的图标，可以考虑用文字来代替图标显示。
# 通过添加 `origin:` 前缀即可显示文字。例如：`origin:知` 会用 `知` 代替图标显示。
social:
  # 如果不需要友链，设为 false 即可直接关闭。
  enable: true
  github: https://github.com/ || github
  google: https://plus.google.com/ || google
  twitter: https://twitter.com/ || twitter
  youtube: https://youtube.com/ || youtube
  segmentfault: https://segmentfault.com/ || origin:sf
  zhihu: https://www.zhihu.com/ || origin:知
  weibo: https://weibo.com/ || weibo
  wechat: yournumber || weixin
  telegram: yournumber || telegram
  qq: yournumber || qq
  # 你可以手动添加这里没有的友链。
  # xxx: xxx || (origin:)xxx

# 友链的一些设置
social_setting:
  # 只显示图标
  icon_only: true
  # 友链之间的排列方式，取值同 CSS 的 "justify-content" 属性。
  # 例如：flex-start | center | flex-end | space-between 等。
  # 更多取值请查看：https://developer.mozilla.org/zh-CN/docs/Web/CSS/justify-content
  text_align: center
```

## 文章目录

``` yml
# Table Of Contents in the Sidebar.
toc:
  enable: true
  # Automatically add list number to toc.
  number: true
  # If true, all words will be placed on next lines
  #   if header width longer then sidebar width.
  wrap: true
  # Maximum heading depth of generated toc.
  #   You can set it in one post through `toc_max_depth` in Front-matter.
  # e.g. value: 3, will use h1~3 to generated toc.
  max_depth: 5
```








## 订阅

- 添加 Email 订阅

修改 `stun.yml` 文件：

``` yaml
feed:
  mail: # url
```

- 添加 RSS 订阅

TODO

## 代码高亮

修改 `stun.yml` 文件：

``` yaml
highlight_theme: light
```

有三种可供选择的代码高亮样式：

- light
- drak
- ocean

默认是 light。效果分别如下：

- `highlight_theme: light`

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190608175153.png)

- `highlight_theme: dark`

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190608175155.png)

- `highlight_theme: ocean`

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190608175154.png)

## 赞赏码

启用或关闭赞赏码，修改 `stun.yml` 文件：

``` yaml
reward:
  enable: true # 设为 false 表示不启用
  qr_img_url:
    alipay: # 填写图片路径或链接
    wechat: # 填写图片路径或链接
```

默认不启用。启用效果如下：

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190608175556.png)

## 菜单图标

启用或关闭导航栏菜单图标，修改 `stun.yml` 文件：

``` yaml
header_menu_icon_show: # true or false
```

默认启用。

## 代码换行

设置代码溢出时，是否换行，修改 `stun.yml` 文件：

``` yaml
code_word_wrap: # true or false
```

默认换行。如果设为不换行，当代码溢出时，显示水平滚动条。

效果分别如下：

- `code_word_wrap: true`

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190608214540.png)

- `code_word_wrap: false`

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190608214539.png)

## 图片水平对齐方式

如果你想设置文章中，图片的水平对齐方式，修改 `stun.yml` 文件：

``` yaml
img_horizonal_align: # left or center or right
```

可选的值有：`left`, `center`, `right`。默认值为空，即不设置。

> 默认情况下，图片显示居左，支持行内显示。如果你手动设置了图片的水平对齐方式，则图片不再支持行内显示。

效果分别如下：

- 设为默认值，即 `img_horizonal_align: `

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190608220937.png)

- `img_horizonal_align: left`

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190608215836.png)

- `img_horizonal_align: center`

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190608215837.png)

- `img_horizonal_align: right`

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190608215838.png)

## 文字与图片的垂直对齐方式

如果你没有手动设置**图片的水平对齐方式**（否则请忽略此配置项），那么图片将支持和文字在同一行内显示。此时，如果你想设置文字与图片的垂直对齐方式，修改 `stun.yml` 文件：

``` yaml
text_vertical_align_with_img: # top or middle or bottom
```

可选的值有：`top`, `middle`, `bottom`。默认值为 `bottom`。

效果分别如下：

- `text_vertical_align_with_img: top`

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190608232755.png)

- `text_vertical_align_with_img: middle`

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190608232756.png)

- `text_vertical_align_with_img: bottom`

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190608232754.png)

## 返回顶部

启用或关闭返回顶部按钮，修改 `stun.yml` 文件：

``` yaml
back_to_top: # true or false
```

默认启用。

## 文章版权声明

设置文章末尾的版权声明，修改 `stun.yml` 文件：

``` yaml
post_copyright:
  enable: true # 设为 false 表示不启用
  license: CC BY-NC-SA 4.0
  license_url: https://creativecommons.org/licenses/by-nc-sa/4.0/
```

默认启用并采用 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 许可协议，效果如下：

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190609092406.png)

## 站点年份

设置网站底部的年份，修改 `stun.yml` 文件：

``` yaml
site_copyright:
  enable: true # 设为 false 表示不启用
  start: 2019
  # 如果不设置，默认是最新的年份
  end: 
```

其中开始时间必须设置，截止时间不设置默认为最新的年份。效果分别如下：

- 设置开始、截止时间

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190609170802.png)

- 设置开始时间，不设置截止时间

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190609170803.png)

- 开始时间和截止时间相同

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190609170801.png)

## 底部自定义文字

设置网站底部自定义文字（支持 HTML 语法），修改 `stun.yml` 文件：

``` yaml
footer_custom_text: 
```

你可以填写任意信息，通常用于填写 ICP 备案号，网站采用的服务等等。

例如，设置为 `Hello there. 博客托管于 <a href="https://github.com/">Github</a>.<br>备案 xxxxxxxxx 号.`，效果如下：

![](https://raw.githubusercontent.com/liuyib/picBed/master/hexo-theme-stun/doc/20190609101330.png)
---
title: hexo配置-打造自己的博客（基于landscape主题）
permalink: hexo+config
toc: true
date: 2019-01-14 16:15:43
tags:
  - Hexo 配置
categories:
  - Hexo
---

## 修改Banner图
替换themes/landscape/source/css/images/banner.jpg下的图片即可。
注意命名一定要是`banner.jpg`

## 修改标题、副标题、博客描述、语言
修改根目录下_config.yml文件
```
# Site
title: Michelle's Home
subtitle: 纳纳的小窝
description: 学习笔记、工作心得
keywords:
author: 江纳纳
language: zh-CN //必须和主题中languages包中文件名相同
timezone:
```
修改之后：
![](home-config.png)

## 对source文件夹下文章md文件分类
我的是按月归档的。操作步骤如下：
1.修改_config.yml文件
```
new_post_name: :year/:month/:title.md
```
2.修改文章模版，增加 permalink一项就好了。文章的模版在scaffolds/post.md，内容修改如下：
```
---
title: {{ title }}
permalink: {{ title }}
date: {{ date }}
tags:
categories: 
toc: false
---
```
而我们使用`hexo new post [title]`创建文章的时候，应注意把标题里的空格换为`-`。
[参考链接](https://blog.csdn.net/maosidiaoxian/article/details/85220394)
## 给文章设置目录
1.修改article.ejs
路径：themes/landscape/layout/_partial/article.ejs
修改前：

```
<div class="article-entry" itemprop="articleBody">
      <% if (post.excerpt && index){ %>
        <%- post.excerpt %>
        <% if (theme.excerpt_link){ %>
          <p class="article-more-link">
            <a href="<%- url_for(post.path) %>#more"><%= theme.excerpt_link %></a>
          </p>
        <% } %>
      <% } else { %>
        <!-- Table of Contents -->
        <%- post.content %>
      <% } %>
    </div>
```
修改后：
```
<div class="article-entry" itemprop="articleBody">
      <% if (post.excerpt && index){ %>
        <%- post.excerpt %>
        <% if (theme.excerpt_link){ %>
          <p class="article-more-link">
            <a href="<%- url_for(post.path) %>#more"><%= theme.excerpt_link %></a>
          </p>
        <% } %>
      <% } else { %>
        <!-- 文章目录 -->
        <% if(!index && post.toc){ %> //!index:表示主页不显示 post.toc表示Font-Formatter中设置了toc
          <div id="toc" class="toc-article">
            <strong class="toc-title">目录</strong>
            <%- toc(post.content,{list_number:false}) %>
          </div>
         <% } %>
        <!-- Table of Contents -->
        <%- post.content %>
      <% } %>
    </div>
```
2.设置目录的样式
文件路径：themes/landscape/source/css/_partial/article.styl，在末尾添加：
```
/*toc*/
.toc-article
  background #eee
  border 1px solid #bbb
  border-radius 3px
  margin 1.5em 0 0.3em 0
  padding 1.2em 1em 0 1em
  max-width 28%
.toc-title
  font-size 120%
#toc
  line-height 1em
  font-size 0.9em
  /*float right*/ //该属性的作用是使目录悬浮到右侧，注释掉之后，目录默认显示在标题和内容之间
  .toc
    padding 0
    margin 1em
    line-height 1.8em
    li
      list-style-type none
  .toc-child 
    margin-left 1em
```
## 插入图片
### 远程图片
将图片上传到某个远程服务器上，然后通过引用图片地址的方式加载图片，引用方式如下：
```
![](https://b-ssl.duitang.com/uploads/item/201411/07/20141107164412_v284V.thumb.1900_0.jpeg)
```
![](https://b-ssl.duitang.com/uploads/item/201411/07/20141107164412_v284V.thumb.1900_0.jpeg)
注：这是markdown默认的引用方式

优点：引用方便，且兼容性好
缺点：依赖于网络，加载速度可能受影响

### 本地图片
加载本地图片有两种方式：
#### 在source下面创建一个images 把图片都放到里面，通过如下方式引用
```
![](/images/hexo-image.jpeg)
```
![](/images/hexo-image.jpeg)

#### 在source/_posts/下生成和文件名相同的文件夹
step1：
将根目录下_config.yml中有<font color="ff0000">post_asset_folder: true</font> 如果是flase 改成true
step2:新建文件insert-image
```
hexo new "insert-image"
```
此时会在source/_posts/目录下生成和`insert-image`同名的文件夹。
```
|--source
    |--_posts
        |--insert-image
        |--insert-image.md
```

将图片放入该文件夹即可。
```
|--source
    |--_posts
        |--insert-image
            |--hexo-image.jpeg
        |--insert-image.md
```
引用方式一：
```
![](hexo-image.jpeg)
```
![](hexo-image.jpeg)
注：括号内只需要填入文件名即可。

引用方式二：
```
{% asset_img hexo-image.jpeg image %}
```
{% asset_img hexo-image.jpeg image %}
注：引用方式二是hexo引擎所支持的方式，并不是markdown语法。
## 修改menu，添加关于
1.修改配置文件`_config.yml`，在菜单中添加`关于`
路径：themes/landscape/_config.yml
```
# Header
menu:
  首页: /
  归档: /archives
  #分类: /categories
  #标签: /tags/
  #随笔: /essay
  关于: /about
```
注意：menu下的菜单项默认是英文，因为我们已经设置了语言为中文，但是显示上并没有变化，这是因为，在landscape主题的语言包中，并没有适配菜单项，所以直接改成中文就可以了，不过这样对以后想适配多语言就比较麻烦了，只能算是当前的一个临时方案。

2.创建页面
```
hexo new page "about"
```
此时source目录下会生成about的文件夹
```
|--source
    |--_posts
        |--about
            |--index
            |--index.md
```
在`index.md`文件中添加关于的信息即可。

## 添加分类
1.修改模板`scaffolds/post.md`
```
---
title: {{ title }}
permalink: {{ title }}
date: {{ date }}
categories:
---
```
2.创建文件
```
hexo new test-category
```
3.在font-formatter中添加分类：
```
title: test-category
permalink: test-category
date: 2019-01-14 15:55:55
categories:
    - hexo config
```
注意：一篇文章只能属于一个分类，如果写成如下形式：
```
title: test-category
permalink: test-category
date: 2019-01-14 15:55:55
categories:
    - hexo config
    - category config
```
则该文章分类属于`/hexo config/category config/
## 添加标签
1.修改模板`scaffolds/post.md`
```
---
title: {{ title }}
permalink: {{ title }}
date: {{ date }}
categories:
tags:
---
```
2.创建文件
```
hexo new test-category
```
3.在font-formatter中添加分类：
```
title: test-category
permalink: test-category
date: 2019-01-14 15:55:55
categories:
tags:
    - aa
    - bb
```
注意：虽然一篇文章只能属于一个分类，但是却可以有多个标签
## 分类、标签显示文章数
将`themes/landscape/_config.yml`中`show_count`参数设成true
```
# widget behavior
archive_type: 'monthly'
show_count: true
```
修改前：
![](category-no-count.png)
修改后：
![](category-with-count.png)

## 给首页文件增加`阅读全文`
### 方式一：使用`<!--more-->` 标记
这个只要在文章中加上`<!--more-->` 标记，该标记以后部分就不在显示了，只有展开全部才显示，这是hexo定义的。
这样每次添加这个标记有点麻烦，也可以自定义添加
### 方式二：自定义添加
缺点：可能导致排版比较混乱
1.修改文件themes/landscape/layout/_partial/article.ejs
```
<div class="article-entry" itemprop="articleBody">
      <% if (post.excerpt && index){ %>
        <%- post.excerpt %>
        <% if (theme.excerpt_link){ %>
          <p class="article-more-link">
            <a href="<%- url_for(post.path) %>#more"><%= theme.excerpt_link %></a>
          </p>
        <% } %>
      <% } else { %>
        <!-- 文章目录 -->
        <% if(!index && post.toc){ %>
          <div id="toc" class="toc-article">
            <strong class="toc-title">目录</strong>
            <%- toc(post.content,{list_number:true}) %>
          </div>
         <% } %>

        <!--摘要-->
        <% var br = post.content.indexOf('\n') %>
        <% if(br < 0 || !index) { %>
          <%- post.content %>
        <% } else { %>
          <%- post.content.substring(0, br) %>
          <% if (theme.excerpt_link) { %>
            <p class="article-more-link">
              <a href="<%- config.root %><%- post.path %>#more"><%= theme.excerpt_link %></a>
            </p>
          <% } %>
        <% } %>

        <!-- Table of Contents -->
        <!--<%- post.content %>-->
      <% } %>
    </div>
```
在class article-entry的else部分，增加摘要判断。

参考：
[站点首页不显示文章全文](https://blog.csdn.net/lewky_liu/article/details/81277337)
[自动添加read more标记](https://twiceyuan.com/2014/05/25/hexo%E8%87%AA%E5%8A%A8%E6%B7%BB%E5%8A%A0readmore%E6%A0%87%E8%AE%B0/)

## 去掉首页文章日期后的分类信息
修改文件themes/landscape/layout/_partial/article.ejs
```
<div class="article-meta">
    <%- partial('post/date', {class_name: 'article-date', date_format: null}) %>
    <!--<%- partial('post/category') %>首页文章日期后面不显示分类-->
</div>
```
默认：
修改后：
{% asset_img delete-category.png gfg %}

## 关于，去掉文章中的日期
Landscape主题，通过`hexo new page pagename`创建的页面，默认是显示日期的，但是像`关于`这种页面，我们并不希望它显示日期，那么就需要修改`article.ejs`，控制日期的显示
1.修改`scaffolds/page.md`，自定义变量`show_date`，将其值设为`false`
```
---
title: {{ title }}
date: {{ date }}
show_date: false
---
```
2.修改`themes/landscape/layout/_partial/article.ejs`，具体如下：
修改前：
```
 <%- partial('post/date', {class_name: 'article-date', date_format: null}) %>
```
修改后：
```
<% if(typeof(post.show_date)!= "undefined" && !post.show_date){ %> //前一个条件是判断变量是否存在，因为之前写的文章里并没有这个变量，但是却是要显示日期的。

      <% }else{ %>
        <%- partial('post/date', {class_name: 'article-date', date_format: null}) %>
        <!--<%- partial('post/category') %>首页文章日期后面不显示分类-->
    <% } %>
```
## 侧边栏显示分类
安装分类插件：
```
npm install hexo-generator-category --save
```
卸载可执行
```
npm uninstall hexo-generator-category --save
```
那样点击侧边栏的分类，将会提示找不到网页
## 侧边栏显示标签
安装标签插件：
```
npm install hexo-generator-tag --save
```

## 站内搜索
https://segmentfault.com/a/1190000011917419
这个应该是和主题相关的，好像需要自己写
待续。。。
## 多语言支持
## 分享
## config文件参数说明
## 其他：
主题修改相关：
https://www.jianshu.com/p/b96fd206571a

## 在菜单中怎讲category和tags，网上查到的这几篇文章并不起作用，还需要再查查看
https://mrcxt.github.io/hexo/%E8%A7%A3%E5%86%B3hexo%E4%B8%8B%E5%88%86%E7%B1%BB%E5%92%8C%E6%A0%87%E7%AD%BE%E6%97%A0%E6%B3%95%E6%98%BE%E7%A4%BA%E7%9A%84%E9%97%AE%E9%A2%98/
https://blog.csdn.net/qq_32337109/article/details/78755662
https://www.jianshu.com/p/a6a72ed6aa2a
## 统计
## 评论

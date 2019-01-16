---
title: 修改NexT主题上一篇、下一篇样式
permalink: next-post-nav
toc: false
date: 2019-01-16 10:54:18
tags: NexT
categories: 主题
---

Next主题上一篇、下一篇的样式默认是左边是上一篇、右边是下一篇；这和我们的习惯正好相反，为了更符合我们的习惯，决定把它调整过来，主要需要修改以下文件
1.`themes/next/source/css/_common/components/post/post-nav.styl`
修改前：
```
.post-nav-next {
  a { padding-left: 5px; }
}

.post-nav-pre {
  text-align: right;

  a { padding-right: 5px; }

  .fa { margin-left: 5px; }
}
```
修改后：
```
.post-nav-pre {
  a { padding-left: 5px; }
}

.post-nav-next {
  text-align: right;

  a { padding-right: 5px; }

  .fa { margin-left: 5px; }
}
```

2.`themes/next/layout/_macro/post.swig`，全文搜索只要这里有`post-nav-next`,所以确定是修改这个文件
修改前：
```
{% if not is_index and (post.prev or post.next) %}
        <div class="post-nav">
          <div class="post-nav-next post-nav-item">
            {% if post.next %}
              <a href="{{ url_for(post.next.path) }}" rel="next" title="{{ post.next.title }}">
                <i class="fa fa-chevron-left"></i> {{ post.next.title }}
              </a>
            {% endif %}
          </div>

          <span class="post-nav-divider"></span>

          <div class="post-nav-prev post-nav-item">
            {% if post.prev %}
              <a href="{{ url_for(post.prev.path) }}" rel="prev" title="{{ post.prev.title }}">
                {{ post.prev.title }} <i class="fa fa-chevron-right"></i>
              </a>
            {% endif %}
          </div>
        </div>
{% endif %}
```
修改后：
```
{% if not is_index and (post.prev or post.next) %}
        <div class="post-nav">
          <div class="post-nav-prev post-nav-item">
            {% if post.prev %}
              <a href="{{ url_for(post.prev.path) }}" rel="prev" title="{{ post.prev.title }}">
                 <i class="fa fa-chevron-left"></i>{{ post.prev.title }}
              </a>
            {% endif %}
          </div>

          <span class="post-nav-divider"></span>

          <div class="post-nav-next post-nav-item">
            {% if post.next %}
              <a href="{{ url_for(post.next.path) }}" rel="next" title="{{ post.next.title }}">
                {{ post.next.title }}<i class="fa fa-chevron-right"></i> 
              </a>
            {% endif %}
          </div>
        </div>
{% endif %}
```

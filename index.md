---
layout: default
---

<div class="teaserimage">
    <div class="teaserimage-image" data-original={% if site.cover %}{{ site.cover }}{% endif %} >
        Teaser Image
    </div>
</div>

<header class="blog-header">
    <div id="RSSview" style='display:none;'></div>
    {% if site.logo %}
      <a class="blog-logo" href="{{site.url}}" style="background-image: url('{{ site.logo }}')"></a>
    {% endif %}
    <h1 class="blog-title"></h1>
    <h2 class="blog-description cjsyingbixingshu" style="color: #000">{{ site.description }}</h2>
    <div class="custom-links">
      {% for social in site.social %}
        {% if social.url %}
            <a class="icon-{{ social.icon }}" href="{{ social.url }}">
                <span class="genericon genericon-{{ social.icon }}"></span>
            </a>
            {% if forloop.last %}
            {% else %}
                &nbsp;&nbsp;·&nbsp;&nbsp;
            {% endif %}
        {% endif %}
      {% endfor %}
      <!--<a href="/about/">About</a>-->
    </div>
</header>

<main class="content" role="main">

    {% if site.tags.featured %}
    <h5 class="index-headline featured"><div class="feature">Featured</div></h5>

    <div class="container featured">
      {% for post in site.tags.featured %}
        <article class="post" itemscope itemtype="http://schema.org/BlogPosting" role="article">
          <div class="article-item">
            <header class="post-header">
              <h2 class="post-title" itemprop="name"><a href="{{ post.url }}" itemprop="url">{{ post.title }}</a></h2>
            </header>
            <section class="post-excerpt" itemprop="description">
              <p><a href="{{ post.url }}" itemprop="url">{{ post.content | strip_html | truncate: 500 }}</a></p>
            </section>
            <div class="post-meta">
              <time datetime="{{ post.date | date_to_long_string }}">{{ post.date | date_to_long_string }}</time>
  <!--            <span class="post-tags-set">on {{#foreach tags}}<span class="post-tag-{{slug}}">{{#if @first}}{{else}}, {{/if}}<a href="/tag/{{slug}}">{{name}}</a></span>{{/foreach}}</span>-->
            </div>
          </div>
        </article>
      {% endfor %}
    </div>

    <h5 class="index-headline normal"><span>Regular</span></h5>
    {% endif %}

    <div class="cf frame">
      {% for post in paginator.posts %}
        <article class="post" itemscope itemtype="http://schema.org/BlogPosting" role="article">
          <div class="article-item">
            <header class="post-header">
              <h2 class="post-title" itemprop="name"><a href="{{ post.url }}" itemprop="url">{{ post.title }}</a></h2>
            </header>
            <section class="post-excerpt" itemprop="description">
              <p><a href="{{ post.url }}" itemprop="url">{{ post.content | strip_html | truncate: 250 }}</a></p>
            </section>
            <div class="post-meta">
              <time datetime="{{ post.date | date_to_long_string }}">{{ post.date | date_to_long_string }}</time>
<!--            <span class="post-tags-set">on {{#foreach tags}}<span class="post-tag-{{slug}}">{{#if @first}}{{else}}, {{/if}}<a href="/tag/{{slug}}">{{name}}</a></span>{{/foreach}}</span>-->
            </div>
          </div>
        </article>
      {% endfor %}
    </div>

    <nav class="pagination" role="navigation">
      {% if paginator.next_page %}
        <a class="newer-posts" href="/page{{paginator.next_page}}">&larr; Older posts</a>
      {% endif %}
      <span class="page-number">Page {{ paginator.page }} of {{ paginator.total_pages }}</span>
      {% if paginator.previous_page %}
        {% if paginator.page == 2 %}
          <a class="older-posts" href="/">Newer posts &rarr;</a>
        {% else %}
          <a class="older-posts" href="/page{{paginator.previous_page}}">Newer posts &rarr;</a>
        {% endif %}
      {% endif %}
    </nav>


    <!-- {{!! After all the posts, we have the previous/next pagination links }}
    {{pagination}} -->

</main>
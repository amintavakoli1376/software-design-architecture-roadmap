---
layout: default
title: مقالات من
---

# سلام 👋

به وب‌سایت شخصی من خوش آمدید.

اینجا درباره **هوش مصنوعی، مهندسی نرم‌افزار، داده و تجربه‌های فنی** می‌نویسم.

## آخرین مقالات

<div class="articles-grid">

{% for post in site.posts %}

<article class="article-card">

    <div class="article-card-content">

        <h2>
            <a href="{{ post.url | relative_url }}">
                {{ post.title }}
            </a>
        </h2>

        <p>
            {{ post.excerpt | strip_html | truncate: 150 }}
        </p>

        <a href="{{ post.url | relative_url }}" class="read-more">
            مطالعه مقاله ←
        </a>

    </div>

</article>

{% endfor %}

</div>
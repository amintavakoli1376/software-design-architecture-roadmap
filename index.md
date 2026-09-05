---
layout: default
title: خانه
---

<section class="hero">

    <div class="hero-content">

        <p class="hero-label">
            👋 سلام، من امین هستم
        </p>

        <h1>
            درباره هوش مصنوعی،
            مهندسی نرم‌افزار و داده می‌نویسم.
        </h1>

        <p class="hero-description">
            اینجا تجربیات، یادداشت‌ها و چیزهایی که در مسیر
            یادگیری و کارم یاد می‌گیرم را منتشر می‌کنم.
        </p>

        <div class="hero-actions">

            <a href="{{ '/articles/' | relative_url }}" class="btn-primary">
                مشاهده مقالات
            </a>

        </div>

    </div>

</section>


<section class="topics">

    <h2>موضوعات</h2>

    <div class="topic-grid">

        <div class="topic-card">
            <span>🤖</span>
            <h3>هوش مصنوعی</h3>
            <p>
                LLM، RAG، Machine Learning و تکنولوژی‌های AI
            </p>
        </div>

        <div class="topic-card">
            <span>🏗️</span>
            <h3>مهندسی نرم‌افزار</h3>
            <p>
                Software Design، Architecture و Design Patterns
            </p>
        </div>

        <div class="topic-card">
            <span>📊</span>
            <h3>داده</h3>
            <p>
                Data Analysis، SQL و مباحث مرتبط با داده
            </p>
        </div>

    </div>

</section>


<section class="latest-articles">

    <div class="section-header">

        <h2>آخرین مقالات</h2>

        <a href="{{ '/articles/' | relative_url }}">
            مشاهده همه ←
        </a>

    </div>


    <div class="articles-grid">

        {% for post in site.posts limit:4 %}

        <article class="article-card">

            <div class="article-card-content">

                <h2>
                    <a href="{{ post.url | relative_url }}">
                        {{ post.title }}
                    </a>
                </h2>

                {% if post.description %}
                <p>
                    {{ post.description }}
                </p>
                {% endif %}

                {% if post.categories %}
                <div class="article-category">
                    {{ post.categories | first }}
                </div>
                {% endif %}

                {% if post.tags %}
                <div class="article-tags">

                    {% for tag in post.tags %}

                    <span class="article-tag">
                        #{{ tag }}
                    </span>

                    {% endfor %}

                </div>
                {% endif %}

                <a href="{{ post.url | relative_url }}" class="read-more">
                    مطالعه مقاله ←
                </a>

            </div>

        </article>

        {% endfor %}

    </div>

</section>
---
layout: default
title: خانه
---

<section class="home-page">

    <header class="home-intro">

        <div class="home-eyebrow">
            AI · SOFTWARE · DATA
        </div>

        <h1>
            یادداشت‌هایی درباره تکنولوژی،
            مهندسی نرم‌افزار و داده
        </h1>

        <p>
            اینجا تجربیات، یادداشت‌ها و چیزهایی را که
            در مسیر یادگیری و کارم یاد می‌گیرم می‌نویسم.
        </p>

    </header>


    <section class="home-section">

        <div class="section-heading">

            <h2>
                آخرین مقالات
            </h2>

            <a href="{{ '/articles/' | relative_url }}">
                همه مقالات ←
            </a>

        </div>


        <div class="article-list">

            {% for post in site.posts limit:6 %}

            <article class="article-list-item">

                <div class="article-list-meta">

                    {% if post.categories %}

                    <span class="list-category">
                        {{ post.categories | first }}
                    </span>

                    {% endif %}

                    <span>
                        {{ post.date | date: "%Y/%m/%d" }}
                    </span>

                </div>


                <h3>

                    <a href="{{ post.url | relative_url }}">
                        {{ post.title }}
                    </a>

                </h3>


                {% if post.description %}

                <p>
                    {{ post.description }}
                </p>

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

            </article>

            {% endfor %}

        </div>

    </section>

</section>
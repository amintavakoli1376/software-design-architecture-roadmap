---
layout: default
title: مقالات
---

<h1>مقالات</h1>

<p>
تمام مقالات منتشرشده در این وب‌سایت
</p>

<div class="search-box">

    <input
        type="search"
        id="search-input"
        placeholder="جستجو در مقالات..."
        aria-label="جستجو در مقالات"
    >

    <p id="search-count" class="search-count"></p>

</div>

<div class="articles-grid" id="articles-grid">

{% for post in site.posts %}

<article
    class="article-card"
    data-search="
        {{ post.title }}
        {{ post.description }}
        {{ post.content | strip_html }}
        {{ post.categories | first }}
        {{ post.tags | join: ' ' }}
    "
>

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

<script>

document.addEventListener("DOMContentLoaded", async function () {

    const input = document.getElementById("search-input");
    const grid = document.getElementById("articles-grid");
    const count = document.getElementById("search-count");

    if (!input || !grid) return;

    let posts = [];

    try {

        const response = await fetch(
            "{{ '/search.json' | relative_url }}"
        );

        posts = await response.json();

    } catch (error) {

        console.error("خطا در دریافت اطلاعات مقالات:", error);

        return;
    }


    function normalize(text) {

        return String(text || "")
            .toLowerCase()
            .replace(/ي/g, "ی")
            .replace(/ى/g, "ی")
            .replace(/ك/g, "ک")
            .replace(/\s+/g, " ")
            .trim();

    }


    function renderPosts(items) {

        grid.innerHTML = "";

        items.forEach(function (post) {

            const article = document.createElement("article");

            article.className = "article-card";


            const content = document.createElement("div");

            content.className = "article-card-content";


            const title = document.createElement("h2");

            const titleLink = document.createElement("a");

            titleLink.href = post.url;

            titleLink.textContent = post.title;

            title.appendChild(titleLink);

            content.appendChild(title);


            if (post.description) {

                const description = document.createElement("p");

                description.textContent = post.description;

                content.appendChild(description);

            }


            if (post.category) {

                const category = document.createElement("div");

                category.className = "article-category";

                category.textContent = post.category;

                content.appendChild(category);

            }


            if (post.tags) {

                const tags = document.createElement("div");

                tags.className = "article-tags";


                post.tags
                    .split(",")
                    .map(tag => tag.trim())
                    .filter(Boolean)
                    .forEach(function (tag) {

                        const tagElement =
                            document.createElement("span");

                        tagElement.className = "article-tag";

                        tagElement.textContent = "#" + tag;

                        tags.appendChild(tagElement);

                    });


                content.appendChild(tags);

            }


            const readMore = document.createElement("a");

            readMore.href = post.url;

            readMore.className = "read-more";

            readMore.textContent = "مطالعه مقاله ←";

            content.appendChild(readMore);


            article.appendChild(content);

            grid.appendChild(article);

        });


        if (items.length === 0) {

            grid.innerHTML = `
                <p>
                    مقاله‌ای پیدا نشد.
                </p>
            `;

        }


        count.textContent =
            `${items.length} مقاله`;

    }


    renderPosts(posts);


    input.addEventListener("input", function () {

        const query = normalize(this.value);


        if (!query) {

            renderPosts(posts);

            return;

        }


        const terms = query.split(" ");


        const results = posts.filter(function (post) {

            const searchableText = normalize(
                [
                    post.title,
                    post.description,
                    post.content,
                    post.category,
                    post.tags
                ].join(" ")
            );


            return terms.every(function (term) {

                return searchableText.includes(term);

            });

        });


        renderPosts(results);

    });

});

</script>
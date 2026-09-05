---
layout: default
---

<article class="article-page">

    <header class="article-header">

        {% if page.categories %}

        <div class="article-eyebrow">

            {{ page.categories | first }}

        </div>

        {% endif %}


        <h1 class="article-title">
            {{ page.title }}
        </h1>


        {% if page.description %}

        <p class="article-description">
            {{ page.description }}
        </p>

        {% endif %}


        <div class="article-meta">

            <span>
                {{ site.author }}
            </span>

            <span class="meta-separator">·</span>

            <span>
                {{ page.date | date: "%Y/%m/%d" }}
            </span>

            <span class="meta-separator">·</span>

            <span>

                {% assign words = content | number_of_words %}
                {% assign reading_time = words | divided_by: 200 %}

                {% if reading_time < 1 %}
                    ۱
                {% else %}
                    {{ reading_time }}
                {% endif %}

                دقیقه مطالعه

            </span>

        </div>


        {% if page.tags %}

        <div class="article-tags">

            {% for tag in page.tags %}

            <span class="article-tag">
                #{{ tag }}
            </span>

            {% endfor %}

        </div>

        {% endif %}

    </header>


    {% if page.toc %}

    <aside class="table-of-contents">

        <div class="toc-title">
            فهرست مطالب
        </div>

        <ul id="toc"></ul>

    </aside>

    {% endif %}


    <div class="article-content">

        {{ content }}

    </div>


    <div class="article-back">

        <a href="{{ '/articles/' | relative_url }}">
            ← بازگشت به همه مقالات
        </a>

    </div>

</article>


{% if page.toc %}

<script>

document.addEventListener("DOMContentLoaded", function () {

    const content =
        document.querySelector(".article-content");

    const toc =
        document.querySelector("#toc");

    if (!content || !toc) return;


    const headings =
        content.querySelectorAll("h2, h3");


    headings.forEach(function (heading, index) {

        const id =
            "section-" + index;

        heading.id = id;


        const li =
            document.createElement("li");

        if (heading.tagName === "H3") {
            li.classList.add("toc-h3");
        }


        const link =
            document.createElement("a");

        link.href =
            "#" + id;

        link.textContent =
            heading.textContent;


        li.appendChild(link);

        toc.appendChild(li);

    });

});

</script>

{% endif %}
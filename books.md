---
layout: page
title: Books
permalink: /books/
---

{{site.data[site.active_lang].books-page.notes}}

<!-- >> *{{site.data[site.active_lang].books-page.wip}}* -->

## {{site.data[site.active_lang].books-page.current_title}}

{% for cur_book in site.data.books.current %}
    {% if site.active_lang == site.default_lang %}
        {% if cur_book.en %}
- **{{ cur_book.author }}**, *{{ cur_book.original }}* ({{ cur_book.en }})
        {% else %} 
- **{{ cur_book.author }}**, *{{ cur_book.original }}*
        {% endif %}
    {% elsif site.active_lang == "it" %}
- **{{ cur_book.author }}**, *{{ cur_book.it }}*
    {% endif %}
{% endfor %}

## {{site.data[site.active_lang].books-page.read_title}}

#### *{{site.data[site.active_lang].books-page.novel_title}}*

{% for novelist in site.data.books.novels %}

    {% if site.active_lang == site.default_lang %}

        {% if novelist.books.size == 1 %}
            {% if novelist.books[0].en %}
- **{{ novelist.author }}**, *{{ novelist.books[0].original }}* ({{ novelist.books[0].en }})
            {% else %}
- **{{ novelist.author }}**, *{{ novelist.books[0].original }}*
            {% endif %}
        {% else %}
- **{{ novelist.author }}**
        {% for nov_book in novelist.books %}
            {% if nov_book.en %}
    - *{{ nov_book.original }}* ({{ nov_book.en }})
            {% else %} 
    - *{{ nov_book.original }}*
            {% endif %}
        {% endfor %}
    {% endif %}

    {% elsif site.active_lang == "it" %}

        {% if novelist.books.size == 1 %}
- **{{ novelist.author }}**, *{{ novelist.books[0].it }}*
        {% else %}
- **{{ novelist.author }}**  
        {% for nov_book in novelist.books %}
    - *{{ nov_book.it }}*
        {% endfor %}
        {% endif %}
    {% endif %}

{% endfor %}

#### *{{site.data[site.active_lang].books-page.essay_title}}*

{% for essay in site.data.books.essays %}

    {% if site.active_lang == site.default_lang %}

        {% if essay.books.size == 1 %}
            {% if essay.books[0].en %}
- **{{ essay.author }}**, *{{ essay.books[0].original }}* ({{ essay.books[0].en }})
            {% else %}
- **{{ essay.author }}**, *{{ essay.books[0].original }}*
            {% endif %}
        {% else %}
- **{{ essay.author }}**
        {% for es_book in essay.books %}
            {% if es_book.en %}
    - *{{ es_book.original }}* ({{ es_book.en }})
            {% else %} 
    - *{{ es_book.original }}*
            {% endif %}
        {% endfor %}
    {% endif %}

    {% elsif site.active_lang == "it" %}

        {% if essay.books.size == 1 %}
- **{{ essay.author }}**, *{{ essay.books[0].it }}*
        {% else %}
- **{{ essay.author }}**  
        {% for es_book in essay.books %}
    - *{{ es_book.it }}*
        {% endfor %}
        {% endif %}
    {% endif %}

{% endfor %}
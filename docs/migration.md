---
layout: page
title: Migration
description: "В этом документе пошагово описано, как обновить Hydejack с предыдущих версий (v5).\r

  \r

  {% raw %}"
hide_description: true
sitemap: false
---

В этом документе пошагово описано, как обновить Hydejack с предыдущих версий (v5).

К сожалению, обновление с v5 и более ранних версий не является простым процессом. Многие шаблоны и названия изменились по разным причинам, включая лучшую интеграцию с остальной экосистемой Jekyll и упрощенные рабочие процессы, обеспечиваемые коллекциями Jekyll.

0. this unordered seed list will be replaced by toc as unordered list
{:toc}

## С v5
### Обновление структуры папок
Скопируйте следующие папки и файлы из Hydejack v6 в существующий репозиторий. Убедитесь, что вы объединили содержимое папок.

* `_data/`
* `_includes/`
* `_layouts/`
* `_sass/`
* `assets/`
* `index.html` (`index.md`\*)
* `Gemfile`
* `Gemfile.lock`

Обратите внимание, что папка `public` была переименована в `assets`.
Вам нужно будет переместить туда свои статические ресурсы.

### Обновление конфигурации
Файл `_config.yml` значительно изменился. Откройте его и внесите следующие изменения.

1. Переименуйте следующие ключи.

    * `font_accent` => `font_heading`
    * `load_google_fonts` => `google_fonts`
    * `google_analytics_id` => `google_analytics`

2. Включите Jekyll Collections для категорий и тегов, добавив

    ~~~yml
    collections:
      featured_categories:
        permalink: /category/:name/
        output:    true
      featured_tags:
        permalink: /tag/:name/
        output:    true
    ~~~

3. Удалите `photo` и `photo2x` из ключа автора и добавьте вместо них хеш `picture`, который выглядит следующим образом:

    ~~~yml
    picture:
      path: <photo>
      srcset:
        1x: <photo>
        2x: <photo2x>
    ~~~

Если у вас всего одна фотография, вы можете просто указать URL напрямую, например, `picture: <url>`.

Дополнительную информацию см. в разделе [Добавление автора](config.md#adding-an-author).

4. Переименуйте `gems` в `plugins` и убедитесь, что список содержит `jekyll-seo-tag`.

    ~~~yml
    plugins:
      - jekyll-seo-tag
    ~~~


При внесении изменений в `_config.yml` необходимо перезапустить процесс Jekyll, чтобы изменения вступили в силу.

{:.note}

### Восстановление тегов
1. Удалите папку `tag`.

2. Создайте папку верхнего уровня с именем `_featured_tags`.

3. Для каждой записи в `_data/tags.yml` создайте файл Markdown в `_features_tags` с именем тега в качестве имени файла,
например, `hyde.md` для тега "hyde".

4. Для каждого тега скопируйте его содержимое из `_data/tags.yml` в метаданные нового файла, например,

    ~~~yml
    ---
    layout: list
    name: Hyde
    description: >
      Hyde is a brazen two-column Jekyll theme...
    accent_image: /hydejack/public/img/hyde.jpg
    accent_color: '#949667'
    ---
    ~~~
При внесении изменений в `_config.yml` необходимо перезапустить процесс Jekyll, чтобы изменения вступили в силу.

{:.note}

Обратите внимание, что `image` был переименован в `accent_image`, а `color` — в `accent_color`.

5. Добавьте `layout: list` в метаданные.

6. После того, как вы скопировали все теги в отдельные файлы, удалите `_data/tags.yml`.

### Восстановление записей боковой панели
Теперь Hydejack может ссылаться на любые страницы в боковой панели.

1. Удалите `sidebar_tags` в `_config.yml`.

2. Откройте файл, страницу которого вы хотите добавить в боковую панель. Если вы хотите добавить тег, откройте `_featured_tags/<tagname>.md`.

3. Добавьте `menu: true` в метаданные.

4. (Необязательно) Установите `order: <number>`, где `<number>` — это номер, под которым вы хотите, чтобы отображалась ссылка.

### Восстановление RSS-ленты
Теперь лента предоставляется плагином `jekyll-feed` вместо пользовательского решения.

1. Удалите `atom.xml`
2. Добавьте `-jekyll-feed` к `gems` в `_config.yml`, например:

    ~~~yml
    gems:
      - jekyll-seo-tag
      - jekyll-feed
    ~~~

3. (Необязательно) Добавьте следующее в файл `_config.yml`, чтобы лента отображалась по тому же URL-адресу, что и старый `atom.xml`.ig.yml`, например:

    ~~~yml
    feed:
      path: atom.xml
    ~~~

### Восстановление комментариев
Способ включения комментариев немного изменился.
Теперь их необходимо включать для каждой страницы отдельно, добавив `comments: true` в метаданные (это рекомендуется в [руководстве по интеграции Disqus](https://disqus.com/admin/install/platforms/jekyll/)).

Чтобы включить их для всех записей, добавьте в файл конфигурации

```yml
defaults:
  - scope:
      type: posts
    values:
      comments: true
```

### Восстановление страницы «О нас»
В Hydejack теперь есть специальный макет для страниц «О нас».
Чтобы использовать его, откройте файл `about.md` и измените `layout` в метаданных на `about`,
и удалите `{% raw %}{% include about-short.html author=site.author %}{% endraw %}`.

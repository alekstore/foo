---
layout: page
title: Basics
description: В этой главе рассматриваются основы создания контента с помощью Hydejack.
hide_description: true
sitemap: false
---

В этой главе рассматриваются основы создания контента с помощью Hydejack.

0. Этот неупорядоченный список начальных значений будет заменен на оглавление в виде неупорядоченного списка.
{:toc}


## Добавление изображений
Добавление качественных изображений — ключ к привлекательному интерфейсу блога. Вы можете указать атрибут `image` в метаданных записей, страниц и проектов*, который будет использоваться Hydejack различными способами,
например, в качестве изображения заголовка в макетах `блог` и `запись`, предварительного просмотра в социальных сетях, карточек в макетах `сетка` и `проекты`*, миниатюр в выпадающем списке поиска* и т. д.

Атрибут `image` принимает URL-адрес изображения, но рекомендуется вместо этого указывать хеш `path` / `srcset`, например:

```yml
image:
  path:    /assets/img/projects/hyde-v2.jpg
  srcset:
    1920w: /assets/img/projects/hyde-v2.jpg
    960w:  /assets/img/projects/hyde-v2@0,5x.jpg
    480w:  /assets/img/projects/hyde-v2@0,25x.jpg
```

Hydejack будет отображать изображение в различных размерах в зависимости от доступной ширины экрана, поэтому ни один размер не подойдет для всех.
Вместо этого я рекомендую использовать подход, подобный [mipmap], предоставляя изображение в нескольких размерах, причем каждое изображение будет вдвое уже предыдущего.
Поскольку Hydejack предоставляет соответствующий атрибут [`sizes`][mdn-sizes], браузер может выбрать лучшее изображение из предоставленного набора исходных изображений.

Если у вас установлен [ImageMagick], вы можете использовать следующие команды для создания изображений размером 50%, 25% и 12,5% от исходного изображения.
Другие инструменты для работы с изображениями предоставляют аналогичные возможности.

    convert your-image.jpg -resize 50% -sampling-factor 4:2:0 -strip -quality 85 -interlace JPEG -colorspace RGB your-image@0,5x.jpg
    convert your-image.jpg -resize 25% -sampling-factor 4:2:0 -strip -quality 85 -interlace JPEG -colorspace RGB your-image@0,25x.jpg
    convert your-image.jpg -resize 12.5% -sampling-factor 4:2:0 -strip -quality 85 -interlace JPEG -colorspace RGB your-image@0,125x.jpg

Обратите внимание, что ключи в хеше `srcset` должны быть допустимыми «дескрипторами» (как определено [здесь][mdn-srcset]). На практике это означает ширину в пикселях, за которой следует `w`.

Ключ `path` — это резервное изображение для браузеров, которые не поддерживают атрибут `srcset`. Он также используется `jekyll-seo-tag` для предварительного просмотра в социальных сетях.

Для получения дополнительной информации о `srcset` см. [документацию на MDN][mdn-srcset] или [эту статью с CSS-Tricks][csstricks].

[imagemagick]: https://imagemagick.org/index.php
[mipmap]: https://en.wikipedia.org/wiki/Mipmap
[mdn-srcset]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#attr-srcset
[mdn-sizes]: https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#attr-sizes
[csstricks]: https://css-tricks.com/responsive-images-youre-just-changing-resolutions-use-srcset/



## Добавление записи в боковую панель
Чтобы добавить ссылки в боковую панель, заполните поле `menu` в файле `_config.yml` списком пар `title`-`url`, например:

```yml
# file: `_config.yml`
menu:
  - title: Blog
    url:   /blog/
  - title: Projects
    url:   /projects/
  - title: Resume
    url:   /resume/
  - title: About
    url:   /about/
```

### Добавление ссылки на внешнюю страницу в боковую панель
Чтобы добавить ссылки на внешние сайты, просто укажите полный URL-адрес, например:

```yml
menu:
  - title: "@qwtel"
    url:   https://qwtel.com/
``` 

## Добавление категории или тега
Hydejack позволяет использовать макеты `list` или `grid` для отображения всех записей определенной категории или тега.

Прежде чем начать, убедитесь, что ваши конфигурационные файлы содержат коллекции `features_categories` и `featured_tags`:

~~~yml
# file: `_config.yml`
collections:
  featured_categories:
    permalink:         /:name/
    output:            true
  featured_tags:
    permalink:         /tag-:name/
    output:            true
~~~

### Краткий обзор: Категории и теги в Jekyll
В Jekyll записи могут принадлежать к одной или нескольким категориям, а также к одному или нескольким тегам. Они определяются в метаданных записи:

~~~yml
---
layout:     post
title:      Welcome to Jekyll
categories: [jekyll, update]
tags:       [jekyll, update]
---
~~~

Записи также можно отнести к категории в зависимости от их положения в структуре папок, например:

~~~
├── jekyll
│   └── update
│       └── _posts
│           └── 2017-04-07-welcome-to-jekyll.markdown
~~~

Это поместит "Добро пожаловать в Jekyll" в категории `jekyll` и `update`.

Теперь это предпочтительный способ назначения категорий в Hydejack, поскольку он позволяет URL-адресам более естественно соответствовать базовой структуре папок.

{:.note}

Независимо от того, используете вы этот метод или нет, категории всегда будут частью URL-адреса записи, в то время как теги — нет.

Type       | URL
-----------|----
Categories | `/jekyll/update/2017-04-07-welcome-to-jekyll/`
Tags       | `/2017-04-07-welcome-to-jekyll/`
{:.scroll-table-small}
С точки зрения Джекила, это единственное различие.

### Категории и теги в Hydejack
Категории и теги отображаются Hydejack под заголовком, после даты. Категории отображаются с предлогом «in», а теги — с предлогом «on», например:

Type       | Title
-----------|------
Categories | Welcome to Jekyll¬ 07 Apr 2017 **in** Jekyll / Update
Tags       | Welcome to Jekyll¬ 07 Apr 2017 **on** Jekyll, Update
Both       | Welcome to Jekyll¬ 07 Apr 2017 **in** Jekyll / Update **on** Jekyll, Update
{:.scroll-table-small}

Вы можете настроить эти параметры в файле [`_data/string.yml`][strings].

### Создание новой категории или тега
По умолчанию категории и теги отображаются как обычный текст. Для того чтобы они вели на страницу со списком всех записей, относящихся к этой категории или тегу, необходимы дополнительные шаги.

Для каждой рекомендуемой категории или тега необходимо создать файл с именем `<category-name>.md` или `<tag-name>.md` в папках `_featured_tags` и `_featured_categories` соответственно. Каждый файл в этих папках является частью [коллекции Jekyll](https://jekyllrb.com/docs/collections/).

Метаданные категории или тега задаются в метаданных файлов, например:

~~~yml
# file: `_featured_categories/hyde.md`
---
layout: list
title:  Hyde
slug:   hyde
description: >
  Hyde is a brazen two-column [Jekyll](http://jekyllrb.com) theme.
  It's based on [Poole](http://getpoole.com), the Jekyll butler.
---
~~~

`layout`
: Must either `list` or `grid`\*

`title`
Используется в качестве заголовка страницы, а также названия категории или тега в строке под заголовком записи в блоге. Может отличаться от названия тега или категории, если `slug` совпадает с названием.

`slug`
: Должно быть идентично ключу, используемому в метаданных блога, т.е. если вы используете `categories: [jekyll]`, то `slug` должен быть `jekyll`. По умолчанию slug определяется из заголовка, но здесь рекомендуется задать его явно.

`description`
Описание средней длины, используемое на странице с подробной информацией о теге или категории и отображаемое в поле сообщения под заголовком.

`menu`
Установите значение `true`, если хотите, чтобы категория или тег отображались в боковой панели. Для получения дополнительной информации см. [Добавление записи в боковую панель](#adding-an-entry-to-the-sidebar).

После создания файла страницу можно найти по адресу `/category/<categoryname>/` или `/tag/<tagname>/`.


## Добавление страницы «О нас»
Страницы «О нас» — часто используемый вариант, поэтому Hydejack имеет для них специальный макет. Это небольшая модификация макета `page`, позволяющая отображать информацию об авторе, добавив маркер `<!--author-->` где-нибудь на странице.

Чтобы создать страницу «О нас», убедитесь, что для параметра `layout` установлено значение `about`.
Дополнительную информацию об авторах см. в разделе [Добавление автора](config.md#adding-an-author)..

~~~md
<!-- file: `about.md` -->
---
layout: about
title:  About
---

Some content

<!--author-->
~~~


## Добавление титульной страницы
В Hydejack 8 появились титульные страницы, то есть страницы с открытой боковой панелью, которая занимает весь экран. Эта функция предназначена для целевых страниц. Чтобы включить её на странице, просто добавьте `cover: true` в метаданные.

![Cover page example](../assets/img/blog/hydejack-8@0,5x.png){:.lead width="960" height="540" loading="lazy"}

~~~yml
# file: `index.md`
---
layout: welcome
title:  Welcome
cover:  true #!! Add this
---
~~~

## Добавление похожих записей к записи
Вы можете выбрать, какие записи будут отображаться в разделе «Похожие записи» под записью, добавив ключ `related_posts` в метаданные записи.

~~~yml
# file: `category/_posts/2020-02-01-some-post.md`
---
layout: post
related_posts:
  # Specify via the path in the file system
  - category/_posts/2020-01-01-other-post.md
  # Can also use the url of the post,
  # but this will break when changing the `permalink` setting!
  - /blog/category/2020-01-02-other-other-post/
---
~~~

## Настройка
### Добавление пользовательского CSS
Самый быстрый и безопасный способ добавить пользовательский CSS в Hydejack — это использовать файлы `_sass/my-inline.scss` и `_sass/my-style.scss` (создайте папку/файлы, если они не существуют).

Чтобы добавить CSS, который будет встроен в страницу, то есть загружен при первом запросе, поместите правила CSS в `my-inline.scss`. Это предназначено для контента, видимого без прокрутки. В противном случае поместите правила CSS в `my-style.scss`.

Обратите внимание, что это различие не имеет эффекта, если включена опция `no_inline_css`.

### Добавление пользовательского HTML в заголовок (<head>)
Чтобы добавить пользовательские HTML-элементы в `<head>` документа, откройте `_includes/my-head.html` (создайте папку/файлы, если они не существуют) и добавьте свои элементы туда.

Например, вы можете добавить пользовательский скрипт отслеживания следующим образом:

~~~html
<!-- file: "_includes/my-head.html" -->
<script defer data-domain="my-domain.com" src="https://plausible.io/js/plausible.js"></script>
~~~


### Добавление пользовательского HTML в тело документа
Чтобы добавить пользовательские HTML-элементы в `<body>` документа, откройте `_includes/my-body.html` (создайте папку/файлы, если они не существуют) и добавьте свои элементы туда.

В более ранней версии Hydejack для достижения той же цели использовался файл `my-scripts.html`.
Тем не менее, в некоторых случаях вам может быть предпочтительнее использовать `my-scripts.html` вместо `my-body.html`, поскольку он не загружает скрипты на страницах перенаправления и игнорируется браузерами < IE10.

{:.note}

## Добавление страницы приветствия*
Если вы приобрели PRO-версию Hydejack, у вас есть доступ к макету `welcome`.
Он предназначен для компактного отображения ваших проектов и записей в блоге.
Технически, это модифицированная версия макета `about`, поэтому она позволяет отображать информацию об авторе там, где размещается маркер `<!--author-->`. [Демонстрация][Добро пожаловать].

Вы можете создать приветственную страницу, создать новый файл Markdown и установить в метаданных макет `welcome`.

```yml
# file: `index.md`
```
layout: welcome
title:  Welcome
cover:  true
---

Без дополнительной настройки приветственная страница будет выглядеть как обычная страница. Однако её можно улучшить с помощью маркеров:
- Чтобы отобразить два последних проекта, добавьте маркер `<!--projects-->` в содержимое страницы.
- Чтобы отобразить четыре последних записи в блоге, добавьте маркер `<!--posts-->` в содержимое страницы.
- (Чтобы отобразить пять последних записей в блоге в виде списка, добавьте маркер `<!--posts_list-->` в содержимое страницы.)

Приветственная страница также поддерживает выбор конкретных проектов и записей путем добавления их в метаданные, например:

~~~yml
# file: `index.md`
---
selected_projects:
  - _projects/hydejack-v6.md
  - /projects/hyde-v2/
projects_page: projects.md
selected_posts:
  - _posts/2017-05-03-javascripten.md
  - /blog/2012-02-07-example-content/
posts_page: /blog/
featured: false
---
~~~

`selected_projects`
Список путей к проектам, которые должны быть указаны в маркере `<!--projects-->`.

Укажите пути относительно основного каталога без начального `/`,

или URL-адреса в соответствии со схемой, определенной в `permalink`.

`projects_page`
: Путь к главной странице проектов
Либо путь относительно основного каталога без префикса `./`,

либо URL-адрес в соответствии со схемой, определенной в `permalink`.

`selected_posts`
: Список путей к записям блога, которые должны быть выделены в маркере `<!--posts-->` или `<!--posts_list-->`.
Можно указать пути относительно основного каталога без префикса `/`,

или URL-адреса в соответствии со схемой, определенной в `permalink`.

`posts_page`
: Путь к главной странице записей.
Можно указать путь относительно основного каталога без префикса `./`,

или URL-адрес в соответствии со схемой, определенной в `permalink`.

`featured`
: Необязательный параметр. Если `true`, миниатюры проектов будут занимать всю ширину страницы, а не половину.
Этот параметр имеет приоритет над значением `featured` для отдельных проектов,
т.е. он будет применяться ко всей странице.


## Проекты*

### Добавление страницы проектов
На странице проектов будут отображаться все проекты определенной коллекции.

Во-первых, необходимо убедиться, что коллекция `projects` определена в файле `_config.yml`:

~~~yml
# file: `_config.yml`
collections:
  projects:
    permalink: /projects/:path/
    output:    true
~~~

Далее добавьте файл `projects.md` в корневую директорию (вы можете изменить имя/расположение, чтобы оно соответствовало `permalink` коллекции).
Этот файл имеет структуру `projects` (обратите внимание на букву «s» в конце) и должен содержать ключ `show_collection`,
со значением которого является имя коллекции, например:

~~~yml
# file: `projects.md`
---
layout:          projects
title:           Projects*
show_collection: projects
featured:        true
---
~~~

`layout`
Должно быть «проекты».

`title`
Заголовок страницы. Обратите внимание, что это название используется повторно на каждой отдельной странице проекта.

(для ссылки, ведущей обратно на страницу проекта).

`show_collection`
: Название коллекции, которую вы хотите отобразить на этой странице. По умолчанию — `projects`. Подробную информацию о работе с несколькими коллекциями проектов см. в разделе [Организация проектов](#organizing-projects).
`featured`
: Необязательный параметр. Если значение равно `true`, миниатюры проектов будут занимать всю ширину страницы, а не только половину.
Этот параметр имеет приоритет над значением `featured` для отдельных проектов,
то есть он будет применяться ко всей странице.


### Добавление проекта
Проекты организованы с помощью [Jekyll Collections](https://jekyllrb.com/docs/collections/).
Каждый проект генерирует запись в макете проектов ([Demo][projects]), а также собственную страницу с подробной информацией ([Demo][project]).

Каждый проект определяется файлом в каталоге `_projects`.
Метаинформация проекта определяется в метаданных файла. Вы также можете добавить контент в формате Markdown.
Метаданные проекта должны выглядеть следующим образом:

~~~yml
# file: `_projects/hyde-v2.md`
---
layout:      project
title:       Hyde v2*
date:        2 Jan 2014
image:
  path:       /assets/img/projects/hyde-v2@0,25x.jpg
  srcset:
    1920w:   /assets/img/projects/hyde-v2.jpg
    960w:    /assets/img/projects/hyde-v2@0,5x.jpg
    480w:    /assets/img/projects/hyde-v2@0,25x.jpg
caption:     Hyde is a brazen two-column Jekyll theme.
description: >
  Hyde is a brazen two-column [Jekyll](http://jekyllrb.com) theme.
  It's based on [Poole](http://getpoole.com), the Jekyll butler.
links:
  - title:   Demo
    url:     http://hyde.getpoole.com
  - title:   Source
    url:     https://github.com/poole/hyde
featured:    false
---
~~~

`layout`
: Необходимо установить значение `project`

`date`
Минимальное требование — предоставление данных за год. Используется для сортировки проектов.

`image`
Изображение проекта в формате 16:9. Подробнее см. [Добавление изображений](#adding-images).

`caption`
Краткое описание, отображаемое в составе каждой «карточки проекта» в макете «Проекты».

`description`
Описание средней длины, используемое на странице с подробной информацией о проекте в качестве метаописания и отображаемое в виде всплывающего окна под изображением.

`links`
Список пар `title`-`url`, содержащих ссылки на внешние ресурсы, относящиеся к данному проекту.

`author`
: Необязательно. Автор указывается под проектом, аналогично постам.

`featured`
: Необязательно. Если `true`, предварительный просмотр проекта будет занимать всю ширину контента. Вы можете использовать это для проектов, которым следует уделять больше внимания. Вы можете установить/переопределить это для всей страницы, указав `featured` в метаданных (применяется к макетам `projects` и `welcome`).

### Организация проектов
Если вы хотите организовать свои проекты с помощью категорий или тегов, аналогично тому, как вы это делаете с записями, лучший способ сделать это — использовать несколько коллекций. Категории и теги зарезервированы для записей, и добавление их в коллекции не имеет никакого эффекта.

В файле конфигурации по умолчанию предопределена одна коллекция проектов, но мы можем легко добавить дополнительные коллекции следующим образом:

~~~yml
# file: `_config.yml`
collections:
  # The default projects collection
  projects:
    permalink:         /projects/:path/
    output:            true

  # Our new projects collection
  other_projects:
    # Make sure the permalink path is different!
    permalink:         /other-projects/:path/
    output:            true
~~~

Создайте новую папку в корневом каталоге, используя соглашение об именовании `_<имя коллекции>`. В нашем случае это папка `_other_projects`.

В ней создайте элементы коллекции, как показано выше (#adding-a-project).

Этого достаточно для отображения страниц проектов. Чтобы отобразить их все на одной странице, создайте страницу проектов, как описано выше (#adding-a-projects-page), установив ключ `show_collection` на нашу новую коллекцию, например:

```yaml
# file: "other-collection.md"
---
layout: projects
title: Other Projects*
show_collection: other_projects #!!
---
```

Обратите внимание, что имя файла совпадает с путем `other-projects` в определенной выше `permalink`. Это необходимо для обеспечения соответствия каталогов.


## Добавление резюме*
В PRO-версии Hydejack используется обобщенный макет резюме.

[Демо][резюме].

Страница резюме генерируется на основе действительного [JSON-резюме](https://jsonresume.org/), что является хорошей новостью, если у вас уже есть JSON-резюме. В противном случае, есть несколько способов его получить:

* Вы можете редактировать [пример `resume.yml`][resumeyml] непосредственно в `_data`. Он содержит примеры записей для каждого типа записей.

* Вы можете использовать визуальный [редактор JSON-резюме](http://registry.jsonresume.org/).

* Если у вас есть профиль LinkedIn, вы можете попробовать [преобразование LinkedIn в JSON-резюме](https://jmperezperez.com/linkedin-to-json-resume/).

После того, как у вас будет JSON-резюме, поместите его в `_data`.

Для отображения страницы с резюме создайте новый файл Markdown и в заголовке файла установите для параметра `resume` значение из раздела «Сообщения»:

~~~yml
# file: `resume.md`
---
layout: resume
title:  Resume
description: >
  A short description of the page for search engines (~150 characters long).
hide_description: true 
---
~~~

Итоговый файл `resume.json` (минифицированный) можно скачать из папки assets. При локальном запуске его можно найти по адресу: `_site/assets/resume.json`.
{:.note}

### Изменение макета
Вы можете настроить макет резюме, изменив порядок записей в ключах `left_column` и `right_columns` в метаданных, например:

~~~yml
# file: `resume.md`
---
layout: resume
left_column:
  - work
  - volunteer
  - education
  - awards
  - publications
  - references
right_column:
  - languages
  - skills
  - interests
---
~~~

### Значки уровней навыков
По умолчанию в макете некоторые ключевые слова будут заменены значками в виде звездочек. Ключевые слова следующие:

| Icon | Skills | Languages |
|--|--|--|
| <span class="icon-star-full"></span><span class="icon-star-full"></span><span class="icon-star-full"></span>    | 3/3, Master, Expert, Senior, Professional | 5/5, Native or bilingual proficiency, Native speaker |
| <span class="icon-star-full"></span><span class="icon-star-full"></span><span class="icon-star-half"></span>    |                                           | 4/5, Full professional proficiency |
| <span class="icon-star-full"></span><span class="icon-star-full"></span><span class="icon-star-empty"></span>   | 2/3, Intermediate, Advanced, Amateur      | 3/5, Professional working proficiency |
| <span class="icon-star-full"></span><span class="icon-star-half"></span><span class="icon-star-empty"></span>   |                                           | 2/5, Limited working proficiency |
| <span class="icon-star-full"></span><span class="icon-star-empty"></span><span class="icon-star-empty"></span>  | 1/3, Beginner, Novice, Junior             | 1/5, Elementary proficiency |
| <span class="icon-star-empty"></span><span class="icon-star-empty"></span><span class="icon-star-empty"></span> | 0/3                                       | 0/5, No proficiency |
Если ключевое слово не распознано, вместо него будет отображен предоставленный текст. Чтобы отключить значки и всегда отображать текст, установите для параметров `no_skill_icons` и/или `no_langauge_icons` значение `true`.

~~~yml
# file: `resume.md`
no_language_icons: true
no_skill_icons: true
~~~
### Добавление специализированного резюме или нескольких резюме
Вы можете добавить специализированное резюме или несколько резюме, добавив YAML-файл резюме в метаданные под ключом `resume`.

Например:

~~~yml
# file: `resume.md`
---
layout: resume
title:  Resume
description: >
  A short description of the page for search engines (~150 characters long).
resume:
  basics:
    name: "Richard Hendricks"
    label: "Programmer"
    picture: "/assets/icons/icon.png"
  # ...
---
~~~

### Загрузки
Вы можете добавить кнопки, позволяющие читателям распечатать или загрузить ваше резюме в различных форматах.
Добавьте следующий текст в начало текста, чтобы добавить все 4 кнопки:

```yml
# file: "resume.md"
buttons:
  print: true
  pdf: /assets/Resume.pdf
  vcf: http://h2vx.com/vcf/<!--url-->
  json: /assets/resume.json
```

Чтобы удалить кнопку, удалите соответствующий ключ из хеша.

Хотя файл `resume.json` может быть сгенерирован самим Jekyll, а vCard — [внешним сервисом][h2vx],
PDF-файл необходимо предварительно сгенерировать самостоятельно.

Вы можете отобразить PDF-файл прямо со страницы резюме, используя функцию «Печать в PDF» в вашем браузере (лучше всего подходит Chrome).
Для достижения наилучших результатов отметьте следующие параметры во всплывающем окне печати:

[h2vx]: http://h2vx.com/vcf/

![Снимите флажки с «Заголовки и нижние колонтитулы», установите флажок «Фоновая графика».](/assets/img/docs/chrome-print.png){:width="299" height="588" loading="lazy"}


Continue with [Writing](writing.md){:.heading.flip-title}
{:.read-more}

[welcome]: https://hydejack.com/
[resume]: https://hydejack.com/resume/
[projects]: https://hydejack.com/projects/
[project]: https://hydejack.com/projects/default/

[strings]: https://github.com/hydecorp/hydejack-site/blob/master/_data/strings.yml
[resumeyml]: https://github.com/hydecorp/hydejack-site/blob/master/_data/resume.yml

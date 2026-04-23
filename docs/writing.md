---
layout: page
title: Writing
description: "Hydejack предлагает несколько дополнительных функций для разметки вашего контента. Не беспокойтесь, это всего лишь CSS-классы, добавленные с помощью синтаксиса `{:...}` из kramdown, чтобы ваш контент оставался совместимым с другими темами Jekyll.\r

  \r

  Продолжить с [Config](config.md){:.heading.flip-title}\r

  {:.read-more}"
hide_description: true
sitemap: false
---
Hydejack предлагает несколько дополнительных функций для разметки вашего контента.
Не беспокойтесь, это всего лишь CSS-классы, добавленные с помощью синтаксиса `{:...}` из kramdown,
чтобы ваш контент оставался совместимым с другими темами Jekyll.

1. Этот список будет заменен оглавлением
{:toc}

Для общего ознакомления с Markdown см. [Освоение Markdown][mm] и [Синтаксис kramdown][ksyn].

{:.note}

## Несколько слов о скорости сборки
Если скорость сборки является проблемой, попробуйте использовать флаг `--incremental`, например,

    bundle exec jekyll serve --incremental

Из документации Jekyll (https://jekyllrb.com/docs/configuration/#build-command-options) (выделено мной):

> Включите экспериментальную функцию инкрементальной сборки. Инкрементальная сборка перестраивает только измененные записи и страницы, что значительно повышает производительность больших сайтов, *но в некоторых случаях может нарушить генерацию сайта*.

Нарушение происходит при создании новых файлов или изменении имен файлов.
Кроме того, изменение заголовка, категории, тегов и т. д. страницы или записи не будет отражено на страницах,
кроме самой страницы или записи.
Это делает его идеальным для написания новых записей и предварительного просмотра изменений, но не для настройки нового контента.

## Добавление оглавления
Вы можете добавить сгенерированное оглавление на любую страницу, добавив `{:toc}` под списком.

Markdown:
~~~md
* this unordered seed list will be replaced by the toc
{:toc}
~~~

Вы также можете создать оглавление в виде упорядоченного списка (обратите внимание на «1.» вместо «*»):

~~~md
1. this ordered seed list will be replaced by the toc
{:toc}
~~~

Для того чтобы оглавление стало фиксированным, ширина экрана должна быть больше 1665 пикселей.

В противном случае оглавление будет отображаться там, где в документе расположен список исходных данных.
Чтобы отображать оглавление только на больших экранах (> 1665 пикселей), используйте следующее:

~~~md
* this unordered seed list will be replaced by the toc 
{:toc .large-only}
~~~
«Фиксированное» оглавление уменьшит объем пространства, освобождаемого параметром `no_break_layout: false`.
Это необходимо для того, чтобы большие блоки кода или таблицы не перекрывали оглавление.

{:.note}

## Добавление примечаний
Вы можете добавить примечание, добавив класс `note` к абзацу.

Пример:

Вы можете добавить примечание.

{:.note}

Markdown:
~~~markdown
You can add a note.
{:.note}
~~~

Отредактируйте ключ `note` в файле `_data/strings.yml`, чтобы изменить текст метки по умолчанию.
Чтобы добавить заметку с определенной меткой, добавьте атрибут `title`:

~~~markdown
A custom label.
{:.note title="Attention"}
~~~
Пользовательская метка.

{:.note title="Внимание"}

## Добавление крупного текста
Вы можете добавить крупный текст, добавив класс `lead` к абзацу.

Пример:

Вы можете добавить крупный текст.

{:.lead}

Markdown:
~~~markdown
You can add large text.
{:.lead}
~~~
## Добавление больших изображений
Вы можете сделать так, чтобы изображение занимало всю ширину экрана, добавив класс `lead`.

Пример:

![Изображение во всю ширину](https://via.placeholder.com/800x100){:.lead width="800" height="100" loading="lazy"}

Markdown:
Markdown:
~~~markdown
![Full-width image](https://via.placeholder.com/800x100){:.lead width="800" height="100" loading="lazy"}
~~~

IРекомендуется указывать размеры изображения с помощью атрибутов `width` и `height`,
чтобы браузеры могли рассчитать макет до загрузки изображений. Сочетание этого с атрибутом `loading="lazy"`
позволяет современным браузерам загружать изображения непосредственно во время прокрутки пользователем.

В предыдущих версиях Hydejack использовалось собственное решение для отложенной загрузки на основе JavaScript,
но в версии 9 оно было удалено в пользу этого более стандартизированного подхода.

{:.note}

## Добавление подписей к изображениям
Вы можете добавить подписи к большим изображениям, добавив класс `figcaption` к абзацу после изображения:

![Изображение во всю ширину](https://via.placeholder.com/800x100){:.lead width="800" height="100" loading="lazy"}

Необязательная подпись к изображению.

{:.figcaption}

Markdown:Рекомендуется указывать размеры изображения с помощью атрибутов `width` и `height`,
чтобы браузеры могли рассчитать макет до загрузки изображений. Сочетание этого с атрибутом `loading="lazy"`
позволяет современным браузерам загружать изображения непосредственно во время прокрутки пользователем.

В предыдущих версиях Hydejack использовалось собственное решение для отложенной загрузки на основе JavaScript,
но в версии 9 оно было удалено в пользу этого более стандартизированного подхода.

{:.note}

## Добавление подписей к изображениям
Вы можете добавить подписи к большим изображениям, добавив класс `figcaption` к абзацу после изображения:

![Изображение во всю ширину](https://via.placeholder.com/800x100){:.lead width="800" height="100" loading="lazy"}

Необязательная подпись к изображению.

{:.figcaption}

Markdown:
~~~md
![Full-width image](https://via.placeholder.com/800x100){:.lead width="800" height="100" loading="lazy"}

A caption for an image.
{:.figcaption}
~~~

## Добавление больших кавычек
Вы можете сделать так, чтобы кавычка «выделялась», добавив класс `lead`.

Пример:

> Вы можете сделать так, чтобы кавычка «выделялась».

{:.lead}

Markdown:
~~~
> You can make a quote "pop out".
{:.lead}
~~~
## Добавление полупрозрачного текста
Вы можете сделать текст серым, добавив класс `faded`. Используйте его экономно и только для несущественной информации, так как в этом случае текст будет сложнее читаться.

Пример:

Я полупрозрачный, полупрозрачный, полупрозрачный.

{:.faded}

Markdown:
~~~md
I'm faded, faded, faded.
{:.faded}
~~~

## Добавление таблиц
Добавление таблиц — простая процедура, описанная в документации [kramdown docs][ksyntab], например:

| Выравнивание по умолчанию | Выравнивание по левому краю | Выравнивание по центру | Выравнивание по правому краю |

|-----------------|:-----------|:---------------:|---------------:|

| Первая часть текста | Вторая ячейка | Третья ячейка | Четвертая ячейка |

Markdown:
~~~md
| Default aligned |Left aligned| Center aligned  | Right aligned  |
|-----------------|:-----------|:---------------:|---------------:|
| First body part |Second cell | Third cell      | fourth cell    |
~~~

Однако при добавлении больших таблиц ситуация усложняется.
В этом случае Hydejack нарушит макет и предоставит таблице всю доступную ширину экрана справа:

| Default aligned |Left aligned| Center aligned  | Right aligned  | Default aligned |Left aligned| Center aligned  | Right aligned  | Default aligned |Left aligned| Center aligned  | Right aligned  | Default aligned |Left aligned| Center aligned  | Right aligned  |
|-----------------|:-----------|:---------------:|---------------:|-----------------|:-----------|:---------------:|---------------:|-----------------|:-----------|:---------------:|---------------:|-----------------|:-----------|:---------------:|---------------:|
| First body part |Second cell | Third cell      | fourth cell    | First body part |Second cell | Third cell      | fourth cell    | First body part |Second cell | Third cell      | fourth cell    | First body part |Second cell | Third cell      | fourth cell    |
| Second line     |foo         | **strong**      | baz            | Second line     |foo         | **strong**      | baz            | Second line     |foo         | **strong**      | baz            | Second line     |foo         | **strong**      | baz            |
| Third line      |quux        | baz             | bar            | Third line      |quux        | baz             | bar            | Third line      |quux        | baz             | bar            | Third line      |quux        | baz             | bar            |
| Second body     |            |                 |                | Second body     |            |                 |                | Second body     |            |                 |                | Second body     |            |                 |                |
| 2 line          |            |                 |                | 2 line          |            |                 |                | 2 line          |            |                 |                | 2 line          |            |                 |                |
|=================|============|=================|================|=================|============|=================|================|=================|============|=================|================|=================|============|=================|================|
| Footer row      |            |                 |                | Footer row      |            |                 |                | Footer row      |            |                 |                | Footer row      |            |                 |                |
{:.smaller}

Таблицы подстраиваются под размер шрифта! Вы можете уменьшить размер таблицы, добавив CSS-класс `smaller`. Разместите `{:.smaller}` под таблицей Markdown или добавьте `class="smaller"` к HTML-таблице.

{:.note}

### Прокрутка таблицы
Если дополнительного пространства все еще недостаточно, таблица получит полосу прокрутки.
По умолчанию браузер разрывает строки внутри ячеек таблицы, чтобы содержимое поместилось на экране.
Добавив класс `scroll-table` к таблице, вы измените поведение, и она никогда не будет разрывать строки внутри ячеек, например:

| Default aligned |Left aligned| Center aligned  | Right aligned  | Default aligned |Left aligned| Center aligned  | Right aligned  | Default aligned |Left aligned| Center aligned  | Right aligned  | Default aligned |Left aligned| Center aligned  | Right aligned  |
|-----------------|:-----------|:---------------:|---------------:|-----------------|:-----------|:---------------:|---------------:|-----------------|:-----------|:---------------:|---------------:|-----------------|:-----------|:---------------:|---------------:|
| First body part |Second cell | Third cell      | fourth cell    | First body part |Second cell | Third cell      | fourth cell    | First body part |Second cell | Third cell      | fourth cell    | First body part |Second cell | Third cell      | fourth cell    |
| Second line     |foo         | **strong**      | baz            | Second line     |foo         | **strong**      | baz            | Second line     |foo         | **strong**      | baz            | Second line     |foo         | **strong**      | baz            |
| Third line      |quux        | baz             | bar            | Third line      |quux        | baz             | bar            | Third line      |quux        | baz             | bar            | Third line      |quux        | baz             | bar            |
| Second body     |            |                 |                | Second body     |            |                 |                | Second body     |            |                 |                | Second body     |            |                 |                |
| 2 line          |            |                 |                | 2 line          |            |                 |                | 2 line          |            |                 |                | 2 line          |            |                 |                |
|=================|============|=================|================|=================|============|=================|================|=================|============|=================|================|=================|============|=================|================|
| Footer row      |            |                 |                | Footer row      |            |                 |                | Footer row      |            |                 |                | Footer row      |            |                 |                |
{:.smaller.scroll-table}

Вы можете добавить класс `scroll-table` к таблице Markdown, поместив `{:.scroll-table}` непосредственно под таблицей.
Чтобы добавить класс к HTML-таблице, добавьте его к атрибуту `class` тега `table`, например, `<table class="scroll-table">`.

### Маленькие таблицы
Если таблица достаточно мала, чтобы поместиться на экране даже на маленьких экранах, вы можете добавить класс `stretch-table`,
чтобы заставить таблицу использовать всю доступную ширину содержимого. Обратите внимание, что растянутые таблицы больше нельзя прокручивать.

| Выравнивание по умолчанию | Выравнивание по левому краю | Выравнивание по центру | Выравнивание по правому краю |

|-----------------|:-----------|:----------------:|---------------:|

| Первая часть тела | Вторая ячейка | Третья ячейка | Четвертая ячейка |

{:.stretch-table}

Необязательный заголовок для таблицы
{:.figcaption}

Вы можете добавить класс `stretch-table` к таблице в формате Markdown, разместив `{:.stretch-table}` непосредственно под таблицей.
Чтобы добавить класс к HTML-таблице, добавьте его к атрибуту `class` тега `table`, например, `<table class="stretch-table">`.

Как и изображения, вы можете добавить подписи к таблицам, добавив класс `figcaption` к абзацу после таблицы.

~~~md
An optional caption for a table
{:.figcaption}
~~~

{:.smaller.scroll-table}

Вы можете добавить класс `scroll-table` к таблице Markdown, поместив `{:.scroll-table}` непосредственно под таблицей.
Чтобы добавить класс к HTML-таблице, добавьте его к атрибуту `class` тега `table`, например, `<table class="scroll-table">`.

## Добавление блоков кода
Чтобы добавить блок кода без подсветки синтаксиса, просто сделайте отступ в 4 пробела (обычный Markdown).

Для блоков кода с подсветкой кода используйте `~~~<language>`. Этот синтаксис также поддерживается GitHub.
Для получения дополнительной информации и списка поддерживаемых языков см. [Rouge](http://rouge.jneen.net/).

Вы можете присвоить каждому блоку кода имя файла, сделав первую строку в блоке комментарием вида `File: "dir/filename.ext"`. Для заключения имени файла используйте одинарные кавычки `'`, двойные кавычки `"` или обратные кавычки <code>`</code>.

Пример:

~~~js
// file: "code-block.js"
// Example can be run directly in your JavaScript console

// Create a function that takes two arguments and returns the sum of those
// arguments
var adder = new Function("a", "b", "return a + b");

// Call the function
adder(2, 6);
// > 8
~~~
Необязательная подпись для блока кода
{:.figcaption}

Разметка Markdown:

    ~~~js
    // file: "code-block.js"
    // Example can be run directly in your JavaScript console

    // Create a function that takes two arguments and returns the sum of those
    // arguments
    var adder = new Function("a", "b", "return a + b");

    // Call the function
    adder(2, 6);
    // > 8
    ~~~

    An optional caption for a code block
    {:.figcaption}

НЕ используйте синтаксис Jekyll `{ % highlight % } ... { % endhighlight % }`, особенно вместе с опцией `linenos`.
Сгенерированная `таблица` для отображения номеров строк не имеет CSS-класса или какого-либо другого способа отличить её от обычных таблиц,
поэтому применяются указанные выше стили, что приводит к неработающей странице.
Более того, вывод тегов `highlight` даже не является допустимым HTML, поскольку теги `pre` вложены внутрь тегов `pre`,
что приведет к сбою сайта во время минификации.
Вы можете прочитать об этом подробнее [здесь](https://github.com/penibelst/jekyll-compress-html/issues/71) и
[здесь](https://github.com/jekyll/jekyll/issues/4432).

{:.note}

## Добавление математических выражений
Перед добавлением математических блоков убедитесь, что вы [настроили поддержку математических выражений](./config.md#enabling-math-blocks).

### Встроенные блоки
Пример:

Lorem ipsum $$ f(x) = x^2 $$.

Markdown:
~~~md
Lorem ipsum $$ f(x) = x^2 $$.
~~~

### Блок
Пример:

$$
\begin{aligned}
  \phi(x,y) &= \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right) \\[2em]
            &= \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j)            \\[2em]
            &= (x_1, \ldots, x_n)
               \left(\begin{array}{ccc}
                 \phi(e_1, e_1)  & \cdots & \phi(e_1, e_n) \\
                 \vdots          & \ddots & \vdots         \\
                 \phi(e_n, e_1)  & \cdots & \phi(e_n, e_n)
               \end{array}\right)
               \left(\begin{array}{c}
                 y_1    \\
                 \vdots \\
                 y_n
               \end{array}\right)
\end{aligned}
$$

Дополнительная подпись к математическому блоку
{:.figcaption}

Markdown:

~~~latex
$$
\begin{aligned} %!!15
  \phi(x,y) &= \phi \left(\sum_{i=1}^n x_ie_i, \sum_{j=1}^n y_je_j \right) \\[2em]
            &= \sum_{i=1}^n \sum_{j=1}^n x_i y_j \phi(e_i, e_j)            \\[2em]
            &= (x_1, \ldots, x_n)
               \left(\begin{array}{ccc}
                 \phi(e_1, e_1)  & \cdots & \phi(e_1, e_n) \\
                 \vdots          & \ddots & \vdots         \\
                 \phi(e_n, e_1)  & \cdots & \phi(e_n, e_n)
               \end{array}\right)
               \left(\begin{array}{c}
                 y_1    \\
                 \vdots \\
                 y_n
               \end{array}\right)
\end{aligned}
$$

An optional caption for a math block
{:.figcaption}
~~~

KaTeX не поддерживает окружения `align` и `align*`.

Вместо этого следует использовать `aligned`, например, `\begin{aligned} ... \end{aligned}`.

{:.note}

Продолжить с [Scripts](scripts.md){:.heading.flip-title}
{:.read-more}


[mm]: https://guides.github.com/features/mastering-markdown/
[ksyn]: https://kramdown.gettalong.org/syntax.html
[ksyntab]:https://kramdown.gettalong.org/syntax.html#tables
[rtable]: https://dbushell.com/2016/03/04/css-only-responsive-tables/

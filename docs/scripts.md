---
layout: page
title: Scripts
description: Существует два способа добавления сторонних скриптов. Встраивание идеально подходит для одноразовых скриптов, в то время как глобальные скрипты загружаются на каждой странице.
hide_description: true
sitemap: false
---

Существует два способа добавления сторонних скриптов.
[Встраивание](#embedding) идеально подходит для одноразовых скриптов, например, `widgets.js`, который является частью встроенных твитов (см. ниже).

Добавление [глобальных скриптов](#global-scripts) предназначено для скриптов, которые должны загружаться на каждой странице.

0. Этот неупорядоченный список будет заменен на toc как неупорядоченный список
{:toc}

## Встраивание
Hydejack поддерживает встраивание сторонних скриптов непосредственно в контент Markdown. Это будет работать в большинстве случаев, за исключением случаев, когда скрипт не может быть загружен на страницу более одного раза (это произойдет, когда пользователь перейдет на одну и ту же страницу дважды).

Пример:

~~~html
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
<blockquote class="twitter-tweet" data-lang="en">
  <p lang="en" dir="ltr">
    The next version of Hydejack (v6.3.0) will allow embedding 3rd party scripts,
    like the one that comes with this tweet for example.
  </p>
  &mdash; Florian Klampfer (@qwtel)
  <a href="https://twitter.com/qwtel/status/871098943505039362">June 3, 2017</a>
</blockquote>
~~~

<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">The next version of Hydejack (v6.3.0) will allow embedding 3rd party scripts, like the one that comes with this tweet for example.</p>&mdash; Florian Klampfer (@qwtel) <a href="https://twitter.com/qwtel/status/871098943505039362">June 3, 2017</a></blockquote>

## Глобальные скрипты
Если у вас есть скрипты, которые должны быть включены на каждой странице, вы можете добавить их глобально,
открыв (или создав) файл `_includes/my-scripts.html` и добавив их обычным способом:

```html
<!-- file: `_includes/my-scripts.html` -->
<script
  src="https://code.jquery.com/jquery-3.2.1.slim.min.js"
  integrity="sha256-k2WSCIexGzOj3Euiig+TlR8gA0EmPjuc79OEeY5L45g="
  crossorigin="anonymous"></script>
```

Файл `my-scripts.html` будет добавлен в конец тега `body`.

## Регистрация обработчиков событий push-state
При глобальном встраивании скриптов может потребоваться выполнение некоторого кода инициализации после каждой загрузки страницы. Однако проблема с загрузкой страниц на основе push-state заключается в том, что событие `load` больше не сработает. К счастью, компонент push-state в Hydejack предоставляет событие, которое можно прослушивать вместо этого.

```html
<!-- file: `_includes/my-scripts.html` -->
<script>
  document.getElementById('_pushState').addEventListener('hy-push-state-load', function() {
    // <your init code>
  });
</script>
```

Обратите внимание, что приведенный выше код должен выполняться только один раз, поэтому включите его в свой файл `my-scripts.html`.

`hy-push-state-start`
: Происходит после нажатия на ссылку.

`hy-push-state-ready`
: Анимация завершена, ответ обработан, и можно заменить контент.

`hy-push-state-after`
: Старый контент заменен новым.

`hy-push-state-progress`
: Особый случай, когда анимация завершена, но от сервера еще не поступил ответ.
В этот момент появится индикатор загрузки.

`hy-push-state-load`
: Все встроенные теги скриптов вставлены в документ и загрузка завершена.

## Если ничего не помогает
Если вам не удается заставить внешний скрипт работать с подходом Hydejack к загрузке страниц с использованием состояния push,
вы можете отключить состояние push, добавив в свой файл конфигурации:

```yml
# file: `_config.yml`
hydejack:
  no_push_state: true
```


Продолжить с [Build](build.md){:.heading.flip-title}
{:.read-more}

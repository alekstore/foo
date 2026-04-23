---
layout: page
title: Upgrade
description: В этой главе показано, как обновить Hydejack до более новой версии. Способ обновления зависит от способа установки Hydejack.
hide_description: true
sitemap: false
---

В этой главе показано, как обновить Hydejack до более новой версии. Метод зависит от способа установки Hydejack.

0. this unordered seed list will be replaced by toc as unordered list
{:toc}

Перед обновлением до версии 7+ убедитесь, что вы прочитали [CHANGELOG](../CHANGELOG.md){:.heading.flip-title},
особенно часть о [изменении лицензии](../CHANGELOG.md#license-change)!

{:.note}

## Бесплатная версия
Обновление бесплатной версии темы так же просто, как запуск.

```bash
bundle update jekyll-theme-hydejack
```

## PRO-версия

В версии 9 структура сайтов Hydejack PRO изменилась. Если вы хотите обновиться с версии 8 или более ранней,
воспользуйтесь инструкцией по установке для существующих сайтов (./install.md#existing-sites).

Примечание:

Покупатели PRO-версии найдут необходимые для обновления файлы в папке `#jekyll-theme-hydejack` загруженного zip-архива.
Для обновления просто замените существующую папку темы в корневом каталоге вашего сайта новой, затем запустите

```bash
bundle update jekyll-theme-hydejack
```

If you've modified any of Hydejack's files in `#jekyll-theme-hydejack`, your changes will most likely be overwritten
and you have to apply them again. Make sure you've made a backup before overwriting any files.
{:.note title="Important"}

If you've followed the steps to add __Hydejack PRO__ as a git dependency, all you have to do is change the `tag` to the latest version:

~~~ruby
# file: `Gemfile`
gem "jekyll-theme-hydejack", git: "https://github.com/hydecorp/hydejack-pro", tag: "pro/v9.2.1"
~~~

Обратите внимание, что вы также можете определить зависимость Git на основе ветки, что избавляет от необходимости вносить обновления вручную:

~~~ruby
# file: `Gemfile`
gem "jekyll-theme-hydejack", git: "https://github.com/hydecorp/hydejack-pro", branch: "pro/v9"
~~~

## GitHub Pages
При сборке проектов на GitHub Pages обновление Hydejack осуществляется очень просто: достаточно установить значение ключа `remote_theme` в файле `_config.yml` на нужную версию.

```yml
remote_theme: hydecorp/hydejack@v9.2.1
```

Чтобы использовать последнюю версию из ветки `v9` в каждой сборке, вы можете использовать `hydecorp/hydejack@v9`.

Эта настройка работает только с бесплатной версией Hydejack.

**Пользователям PRO-версии** необходимо аккуратно объединить содержимое папки `starter-kit-gh-pages` в загруженном zip-архиве со своими существующими файлами. См. [Развертывание](./deploy.md){:.heading.flip-title} для более удобного использования GitHub Pages, который также работает с PRO-версией.

{:.note}

Продолжить с [Настройка](config.md){:.heading.flip-title}
{:.read-more}
---
layout: page
title: Install
description: HСпособ установки Hydejack зависит от того, создаете ли вы новый сайт или меняете тему существующего.
hide_description: true
sitemap: false
---

Способ установки Hydejack зависит от того, создаете ли вы новый сайт или меняете тему существующего сайта.

Этот неупорядоченный список будет заменен на toc в качестве неупорядоченного списка
{:toc}
Новые сайты
Для новых сайтов лучший способ начать работу с Hydejack — это использовать стартовый набор.
Он включает в себя документированный файл конфигурации и примеры контента, которые помогут вам быстро начать работу.

Если у вас есть учетная запись GitHub, сделайте форк репозитория стартового набора Hydejack.

В противном случае загрузите стартовый набор и распакуйте его содержимое куда-нибудь на вашем компьютере.

Если вы приобрели PRO-версию Hydejack, используйте содержимое папки starter-kit.

Теперь вы можете приступить к локальному запуску.

Существующие сайты
Если у вас есть существующий сайт, который вы хотите обновить до Hydejack, вы можете установить тему через bundler.
Добавьте следующее в ваш Gemfile:

[hsc]: https://github.com/hydecorp/hydejack-starter-kit
[src]: https://github.com/hydecorp/hydejack-starter-kit/archive/v9.2.1.zip
[nfy]: https://app.netlify.com/start/deploy?repository=https://github.com/hydecorp/hydejack-starter-kit
[dtn]: https://www.netlify.com/img/deploy/button.svg


## Существующие сайты
Если у вас есть существующий сайт, который вы хотели бы обновить до Hydejack, вы можете установить тему через Bundler.

Добавьте следующее в ваш `Gemfile`:

~~~ruby
# file: `Gemfile`
gem "jekyll-theme-hydejack"
~~~

Далее, в вашем конфигурационном файле измените параметр `theme` на Hydejack:

~~~yml
# file: `_config.yml`
theme: jekyll-theme-hydejack
~~~

Теперь вы можете перейти к [локальному запуску](#running-locally).

### Для PRO-клиентов
Если вы приобрели __PRO-версию__ Hydejack, скопируйте папку `#jekyll-theme-hydejack` в корневую папку вашего сайта,
и добавьте следующее в ваш `Gemfile`:

~~~ruby
# file: `Gemfile`
gem "jekyll-theme-hydejack", path: "./#jekyll-theme-hydejack"
~~~
Папка начинается с символа `#`, указывающего на то, что она отличается от обычного содержимого Jekyll.
Символ `#` был выбран потому, что это один из четырех символов, игнорируемых Jekyll по умолчанию (`.`, `_`, `#`, `~`).

В качестве альтернативы, если вас добавили в команду ["PRO Customers"](https://github.com/orgs/hydecorp/teams/pro-customers) на GitHub, вы можете добавить __Hydejack PRO__ в качестве зависимости Git:

~~~ruby
# file: `Gemfile`
gem "jekyll-theme-hydejack", git: "https://github.com/hydecorp/hydejack-pro", tag: "pro/v9.2.1"
~~~
Если вы указали своё имя пользователя GitHub при оформлении заказа, вас должны были автоматически добавить в команду. В противном случае вы можете запросить приглашение по адресу [mail@hydejack.com](mailto:mail@hydejack.com).

Примечание:

Для того чтобы Bundle мог получить доступ к приватному репозиторию, необходимо установить переменную окружения с именем __`BUNDLE_GITHUB__COM`__ в значение __`x-access-token:<GH_REPO_PAT>`__, заменив `<GH_REPO_PAT>` на персональный токен доступа GitHub (PAT) с разрешением «repo».

После того, как вы найдёте способ получить доступ к гему `jekyll-theme-hydejack`, в вашем конфигурационном файле измените `theme` на Hydejack:

~~~yml
# file: `_config.yml`
theme: jekyll-theme-hydejack
~~~

Hydejack поставляется с файлом конфигурации по умолчанию, который отвечает за большую часть настроек,
но стоит ознакомиться с [примером файла конфигурации с примечаниями][config] из стартового комплекта, чтобы увидеть, что доступно. Подробнее см. главу [Config](./config.md){:.heading.flip-title}.

{:.note}

Теперь вы можете перейти к [запуск локально](#running-locally).

### Устранение неполадок
Если ваш существующий сайт объединяет файлы темы с вашим контентом (как это было в предыдущих версиях Hydejack/PRO),
убедитесь, что вы удалили следующие папки:

- `_layouts`
- `_includes` 
- `_sass` 
- `assets`

Папка `assets`, скорее всего, содержит файлы темы, а также ваши личные/контентные файлы.
Убедитесь, что удаляете только файлы, относящиеся к старой теме!

## GitHub Pages
По состоянию на сентябрь 2024 года рекомендуемый способ развертывания на GitHub Pages — это использование пользовательского [GitHub Action][gha], который дает вам полный контроль над процессом сборки.
При использовании GH Action никаких дополнительных шагов не требуется, и вы можете перейти к [локальному запуску](#running-locally) или узнать больше в главе [Развертывание](./deploy.md){:.heading.flip-title}.
При этом Hydejack сохраняет обратную совместимость с устаревшим конвейером, и вы можете продолжать его использовать.

{:.note}

Если вы хотите собрать свой сайт, используя устаревший конвейер, вы можете использовать ветку [`gh-pages`][gpb] в репозитории Hydejack Starter Kit.

[ghp]: https://jekyllrb.com/docs/github-pages/
[gpb]: https://github.com/hydecorp/hydejack-starter-kit/tree/gh-pages
[gha]: https://docs.github.com/en/actions

Главное отличие от стандартного стартового комплекта заключается в использовании параметра `remote_theme` в конфигурационном файле.

```yml
# file: `_config.yml`
remote_theme: hydecorp/hydejack@v9.2.1
```

Эта настройка работает только с бесплатной версией Hydejack.
**Пользователям PRO-версии** следует использовать папку `starter-kit-gh-pages` из загруженного zip-архива при использовании устаревшего конвейера сборки GitHub Pages.

`starter-kit-gh-pages` требуется только при развертывании на GitHub Pages через устаревший конвейер сборки.

При использовании [пользовательского действия GitHub](./deploy.md#github-actions) обычный `starter-kit` обеспечивает более чистую и менее загроможденную структуру папок.

`starter-kit`

Убедитесь, что список `plugins` содержит `jekyll-include-cache` (создайте его, если он не существует):

```yml
# file: `_config.yml`
plugins:
  - jekyll-include-cache
```

Для запуска этой конфигурации локально убедитесь, что следующее входит в состав вашего файла конфигурации. `Gemfile`:

```ruby
# file: `Gemfile`
gem "github-pages", group: :jekyll_plugins
```

Обратите внимание, что Hydejack имеет ограниченный набор функций при сборке на GitHub Pages.
В частности, использование математических формул KaTeX не работает при такой сборке.

{:.note}

## Запуск локально
Убедитесь, что вы перешли в каталог, где находится файл `_config.yml`.
Перед первым запуском необходимо загрузить зависимости с [RubyGems](https://rubygems.org/):

~~~bash
$ bundle install
~~~

Обратите внимание, что Hydejack имеет ограниченный набор функций при сборке на GitHub Pages.
В частности, использование математических формул KaTeX не работает при такой сборке.

{:.note}

## Запуск локально
Убедитесь, что вы перешли в каталог, где находится файл `_config.yml`.
Перед первым запуском необходимо загрузить зависимости с [RubyGems](https://rubygems.org/):

Теперь вы можете запустить Jekyll на своем локальном компьютере:

~~~bash
$ bundle exec jekyll serve
~~~

and point your browser to <http://localhost:4000> to see Hydejack in action.


Continue with [Config](config.md){:.heading.flip-title}
{:.read-more}

[config]: https://github.com/hydecorp/hydejack-starter-kit/blob/v9/_config.yml
[upgrade]: upgrade.md

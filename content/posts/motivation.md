---
date: '2025-06-26T20:30:30+03:00'
draft: false
title: 'Установка Hugo и Tailwind - красивый статический генератор сайтов на бесплатном хостинге от GitHub'
menu_title: "Tailwind и Hugo для блога"  
---
# Почему был выбран именно стек Tailwind и Hugo для блога

На самом деле всё просто:

- **Hugo** - для создания статического сайта, так как нет желания переплачивать по несколько тысяч за хостинг (который с каждым годом всё дороже). 
Статические сайты можно размещать на бесплатных хостингах, например: [GitHub Pages](https://pages.github.com/)

- **Tailwind** - мне сразу понравился, когда я увидел готовые компоненты и темы. 
Всё выглядит современно и аккуратно. В отличие от Bootstrap, который я использовал 10 лет в различных проектах - он уже поднадоел и выглядит топорно. 
Может для MVP и админок сойдёт, но в 2025 году с высокой конкуренцией, 
где сервисы борются за внимание пользователя, использовать Bootstrap в качестве витрины для своего сайта - архаизм.

Далее я буду описывать инструкции, как установить Hugo и Tailwind без всяких React, Vue, Angular и т.д.

## Установка и настройка

Мой рабочий компьютер на Linux Ubuntu, с уже установленным Node.js (на этом останавливаться не буду). Все команды выполняю в терминале Linux.

1. Создаем рабочую директорию (рекомендую такую же структуру):
   ```bash
   mkdir Dev
   cd Dev
Создаем новый сайт на Hugo:

bash
hugo new site marketolog-blog --format "yaml"
Где:

marketolog-blog - название проекта

yaml - формат конфигурации (рекомендую, так как позже будет проще работать с docker-compose)

Настраиваем Tailwind CSS:

bash
npm init -y
npm install tailwindcss @tailwindcss/cli
Создаем структуру для стилей:

bash
mkdir -p assets/css
touch assets/css/input.css
В файле input.css добавляем:

css
@import "tailwindcss";
Запускаем обработку Tailwind:

bash
npx @tailwindcss/cli -i ./assets/css/input.css -o ./assets/css/output.css --watch
Запускаем сервер Hugo:

bash
hugo server -D
Создаем основной шаблон (layouts/index.html):

```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  {{ $css := resources.Get "css/output.css" | minify | fingerprint }}
  <link href="{{ $css.RelPermalink }}" rel="stylesheet" integrity="{{ $css.Data.Integrity }}">
</head>
<body>
  <h1 class="text-3xl bg-amber-600 font-bold underline">
    Hello world!!
  </h1>
</body>
</html>
```
Оптимизируем структуру:

Создаем папку для частичных шаблонов:

bash
mkdir -p layouts/partials
Выносим подключение стилей в отдельный файл (например, layouts/partials/head.html)



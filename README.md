# АВИАТОР — финальная статическая версия сайта

Готовый статический сайт для временного размещения на `aviator.aateam.ru`.

## Состав

- `index.html` — основная страница сайта.
- `assets/images/` — изображения, favicon.
- `assets/og/og-image.jpg` — изображение для предпросмотра в соцсетях и мессенджерах.
- `CNAME` — временный домен для GitHub Pages: `aviator.aateam.ru`.
- `.nojekyll` — отключение Jekyll на GitHub Pages.
- `robots.txt`, `sitemap.xml` — базовые SEO-файлы.

## Контакты на сайте

- Телефон: `+7 926 537-41-18`
- Почта: `departure.aviator@gmail.com`
- Соцсеть/ник: `@aviator`

## Как запустить локально

Откройте `index.html` в браузере или запустите локальный сервер:

```bash
python3 -m http.server 8000
```

После этого сайт будет доступен по адресу `http://localhost:8000`.

## Временная публикация на GitHub Pages

1. Создать новый репозиторий.
2. Загрузить все файлы из этой папки в корень репозитория.
3. В настройках репозитория включить GitHub Pages из ветки `main`, папка `/root`.
4. В DNS домена `aateam.ru` добавить CNAME-запись для поддомена `aviator`, указывающую на GitHub Pages.
5. Дождаться выпуска SSL-сертификата в GitHub Pages.

## Проверка HTTPS для `aviator.aateam.ru`

Файл `CNAME` уже содержит нужный пользовательский домен: `aviator.aateam.ru`.

В GitHub Pages для репозитория `rimsh001/aviator` нужно проверить:

1. `Settings → Pages` использует `Build and deployment → Source: Deploy from a branch`.
2. Ветка публикации: `main`, папка: `/root`.
3. В поле `Custom domain` указан `aviator.aateam.ru`.
4. `DNS check` завершён успешно. Если проверка не проходит, сначала исправить DNS-записи ниже и дождаться обновления зоны.
5. После успешного DNS check дождаться выпуска сертификата и включить `Enforce HTTPS`, когда галочка станет доступной.

В DNS-зоне домена `aateam.ru` для поддомена `aviator` должна остаться ровно одна запись:

```text
Тип: CNAME
Имя/Host: aviator
Значение/Target: rimsh001.github.io
```

Для `aviator.aateam.ru` не должно быть конфликтующих записей `A`, `AAAA`, второго `CNAME` или URL/WEB-редиректа на хостинг REG.RU. Такие записи могут мешать GitHub Pages выпустить сертификат и сделать HTTPS доступным.

Проверочные команды после изменения DNS:

```bash
dig aviator.aateam.ru CNAME +short
dig aviator.aateam.ru A +short
dig aviator.aateam.ru AAAA +short
curl -I http://aviator.aateam.ru
curl -I https://aviator.aateam.ru
```

Ожидаемый результат: CNAME возвращает `rimsh001.github.io.`, запросы `A` и `AAAA` не возвращают прямых записей для `aviator.aateam.ru`, а HTTPS отвечает без ошибки сертификата.

## Важно

CTA-кнопки сейчас работают через `mailto:` и `tel:` — это надёжная временная схема без backend. Позже можно подключить форму с отправкой в CRM, Telegram, Google Sheets или почту через серверный обработчик.

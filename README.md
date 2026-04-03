# Telegram Proxy Viewer

Небольшой статический просмотрщик Telegram MTProto‑прокси, который можно хостить на **GitHub Pages**.

Приложение загружает списки RU/EU‑прокси из репозитория
[`kort0881/telegram-proxy-collector`](https://github.com/kort0881/telegram-proxy-collector)
и конвертирует строки вида `tg://proxy?...` в кликабельные ссылки для Telegram (десктоп/мобайл).

## Фичи

- **Загрузка нескольких источников**: `proxy_ru.txt` и `proxy_eu.txt` с `raw.githubusercontent.com`.
- **Дедупликация** ссылок (одинаковые `tg://proxy?...` не дублируются).
- **Фоновая проверка доступности**: для каждого прокси ставится статус
  _«ожидает проверки»_, _«живой»_ или _«не отвечает»_ (best‑effort через HTTP/HTTPS).
- **Поиск/фильтр** по домену / IP / порту / части ссылки.
- **Быстрые действия**:
  - «Открыть в Telegram» (`tg://`‑ссылка);
  - «Копировать ссылку» для конкретного прокси;
  - «Скопировать все tg:// ссылки» сразу.

Весь фронтенд — один `index.html`, без сборки и зависимостей.

## Локальный запуск

Файл можно открыть напрямую, но из‑за CORS могут быть проблемы, поэтому лучше поднять простой HTTP‑сервер.

### Вариант с Python

```bash
cd proxy
python -m http.server 8000
```

После этого страница будет доступна по адресу `http://localhost:8000/index.html`.

## Деплой на GitHub Pages

1. Создайте репозиторий, например `telegram-proxy-viewer`, и положите в корень этот `index.html` (и при желании `README.md`).
2. Запушьте изменения на ветку `main`:

```bash
git add index.html README.md
git commit -m "Initial GitHub Pages proxy viewer"
git push -u origin main
```

3. Включите **GitHub Pages**:
   - `Settings → Pages`;
   - **Source**: `Deploy from a branch`;
   - **Branch**: `main`, папка `/ (root)`.

4. После деплоя приложение будет доступно по адресу:

```text
https://<your-github-username>.github.io/telegram-proxy-viewer/
```

(для аккаунта [`mikovp`](https://github.com/mikovp) это будет
`https://mikovp.github.io/telegram-proxy-viewer/`.)

## Ограничения проверки доступности

Браузер не умеет напрямую проверять MTProto‑порт, поэтому проверка «живости» делается эвристически:

- для порта `80` пробуется `http://host`;
- для порта `443` — `https://host`;
- для остальных портов: сначала `https://host`, затем `http://host`.

Если оба запроса неуспешны или по таймауту — прокси помечается как _«не отвечает»_.
Это не идеальный индикатор реальной доступности MTProto‑прокси, но позволяет быстро отсеять
очевидно мёртвые/недоступные хосты. 


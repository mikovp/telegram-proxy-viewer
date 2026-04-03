# Telegram Proxy Viewer

Простой статический просмотрщик Telegram MTProto‑прокси.

- Загружает RU/EU‑списки из [`kort0881/telegram-proxy-collector`](https://github.com/kort0881/telegram-proxy-collector).
- Конвертирует строки `tg://proxy?...` в кликабельные ссылки (десктоп/мобайл Telegram).
- Для каждого прокси показывает статус: _ожидает проверки_, _живой_ или _не отвечает_ (best‑effort по HTTP/HTTPS).
- Есть поиск по серверу/IP/порту и копирование одной или всех ссылок.

Онлайн‑версия доступна по адресу:

```text
https://mikovp.github.io/telegram-proxy-viewer/
```


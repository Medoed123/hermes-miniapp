# Hermes Mini App — «Мадам Лю» ✨

Telegram Mini App для бота [@edian1_hermes_bot](https://t.me/edian1_hermes_bot) — пульт управления личным Hermes-агентом (модель Kimi K3).

**Live:** https://medoed123.github.io/hermes-miniapp/

## Что внутри (v3.1)
- Консоль-пульт: ввод с слеш-автокомплитом, диктовка (SpeechRecognition), вставка текстовых файлов
- Панель истории запросов (localStorage), лента отправленного, черновики
- Пикеры модели (`/model`) и усилия рассуждений (`/reasoning`), кнопка «＋» новой сессии
- Панель проектов с быстрыми действиями + ссылки на сайты (открываются во внешнем браузере/Safari)
- Отправка команд через `Telegram.WebApp.sendData()` → ответ приходит в чат с ботом

## Инфраструктура
- Хостинг: GitHub Pages (этот репозиторий, ветка master, корень)
- Кнопка меню бота установлена через Bot API `setChatMenuButton` (тип `web_app`)
- **Важно:** gateway Hermes по умолчанию дропает `web_app_data`. В адаптере
  `hermes-agent/plugins/platforms/telegram/adapter.py` есть пользовательский патч
  (помечен `USER PATCH (mini-app)`), регистрирующий `filters.StatusUpdate.WEB_APP_DATA`
  и передающий payload в сессию как текст. Бэкап оригинала: `adapter.py.bak-webappdata`.
  После обновления Hermes патч нужно восстановить.
- Токен бота: `~/.hermes/.env` (`TELEGRAM_BOT_TOKEN`), нигде не светить.

## Деплой
```
git add -A && git commit -m "..." && git push
```
Pages пересобирается ~1 минуту.

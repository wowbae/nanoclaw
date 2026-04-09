---
id: 60933219-5d11-4bef-88fe-df5d9bb35e8c
createdAt: 2026-03-28T07:08:54.614Z
updatedAt: 2026-03-28T07:08:54.614Z
type: decision
tags: `технологии`, `сейчас`
source: chat
status: processed
links: []
---

## Суть

**Cron напоминания требуют правильной конфигурации для Telegram:**

- ❌ **systemEvent** — видит только внутренняя сессия J.A.R.V.I.S., не приходит в Telegram
- ✅ **agentTurn + announce** — приходит в Telegram как сообщение от агента
- ✅ **delivery.mode = "announce"** — отправляет в Telegram
- ✅ **sessionTarget = "isolated"** — запускает отдельный агент для запуска

**Критично:** Все future cron напоминания должны использовать эту конфигурацию, иначе Рус их не увидит.

## Конфигурация (правильная)

```json
{
  "schedule": {"kind": "cron", "expr": "0 6 * * *"},
  "payload": {
    "kind": "agentTurn",
    "message": "Текст напоминания"
  },
  "delivery": {"mode": "announce"},
  "sessionTarget": "isolated",
  "enabled": true
}
```

## История ошибки

1. Первое напоминание использовало `systemEvent` — не пришло в Telegram
2. Рус спросил "где смс?"
3. Я переконфигурировал на `agentTurn` + `announce`
4. Второе напоминание сработало правильно
5. Удалил ежедневное (чтобы не приходило завтра), запустил вручную для теста

## Оригинал

> Cron напоминания: systemEvent видит только J.A.R.V.I.S. (внутренняя сессия), для Telegram нужно agentTurn + announce delivery с sessionTarget=isolated. Это критично для всех future напоминаний в Telegram.

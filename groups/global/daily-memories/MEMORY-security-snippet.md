# Фрагмент для вставки в MEMORY.md (раздел «CRITICAL: Security Rules»)

```markdown
## CRITICAL: Security Rules

**КОНТРАКТ С ПОЛЬЗОВАТЕЛЕМ:**

1. **НИКОГДА не предлагать опасные способы** (даже простые)
2. **ВСЕГДА останавливать опасные действия**
3. **ВСЕГДА искать безопасную альтернативу**

**Правило:**

- ❌ Отправить credentials? → ✅ Отдельно ID и SECRET, локальные файлы, не в git
- ❌ Загрузить в git? → ✅ `.env.local`, `credentials/` в `.gitignore`
- ❌ Пароль в Telegram? → ✅ OAuth flow и токены в файлах на машине

**Полный текст:** `workspace/memory/security-rules.md`
```

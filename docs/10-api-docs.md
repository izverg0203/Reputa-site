# 10-api-docs.md  
## API Documentation — Reputa 2.0 (Frontend → n8n → Supabase)

Документ описывает все публичные и внутренних API-точки, которые используются фронтендом, AI-помощником, формами аудита/демо и сервисами Reputa.

---

# 1. Общая архитектура API

API построено по принципу:

**Frontend → n8n → Supabase / AI-модели → Frontend**

Frontend **не содержит AI-ключей**, вся логика находится в n8n.

## Уровни API:
1. **Public API (Frontend → n8n)**  
   - формы аудита  
   - формы демо  
   - AI-помощник  
   - генерация черновиков AI-ответов  
   - получение демо-отзывов

2. **Private API (n8n → Supabase / AI)**  
   - загрузка отзывов  
   - обновление репутационных метрик  
   - генерация PDF  
   - AI-инференс  

3. **Direct Supabase REST API**  
   - фронтенд подтягивает демо-данные для визуализации  
   - только SELECT запросы  

---

# 2. Public API Endpoints (Frontend → n8n)

Все публичные API реализованы в n8n как Webhooks.

## 2.1. POST `/api/audit-request`
Отправка формы на бесплатный AI-аудит.

**Body (JSON):**
```json
{
  "clinic_name": "Клиника Здоровье",
  "website": "https://example.ru",
  "contact_name": "Мария",
  "phone": "+79998887766",
  "email": "client@gmail.com"
}

# 11-integrations.md  
## Интеграции Reputa 2.0 (Telegram · Email · CRM · PDF · Webhooks)

Этот документ описывает все внешние и внутренние интеграции Reputa:  
— Telegram,  
— Email-рассылка,  
— PDF-генерация,  
— Webhooks,  
— CRM (Amo/Bitrix — в планах),  
— а также логику, как взаимодействуют n8n → Supabase → Frontend.

---

# 1. Общая схема интеграций

```mermaid
flowchart TD

A[Frontend · Next.js] --> B[n8n Webhooks]

B --> C[Telegram Bot]
B --> D[Email SMTP / Brevo]
B --> E[Puppeteer PDF Generator]
B --> F[Supabase Storage]
B --> G[Supabase DB]

C --> H[Менеджеры / Владельцы клиник]


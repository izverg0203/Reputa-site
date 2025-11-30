# 12-n8n-workflows.md  
## N8N Workflows — Полная схема автоматизации Reputa 2.0

Этот документ описывает ВСЕ рабочие процессы n8n, используемые в Reputa 2.0.  
Структура включает:

- общую архитектуру
- дерево workflows
- схемы Mermaid
- входы/выходы каждого процесса
- обработку ошибок
- future workflows (для масштабирования)

---

# 1. Общая структура n8n

Каждый workflow относится к одной из категорий:

1. **AI-процессы**  
2. **Парсинг и обработка отзывов**  
3. **PDF-аудиты**  
4. **Интеграции** (Telegram / Email / Storage / CRM)  
5. **Webhooks (Frontend → n8n)**  
6. **Cron-задачи**  
7. **Логирование и метрики**  

---

# 2. Дерево Workflows

```text
n8n/
│
├── 01_frontend_webhooks/
│     ├── audit-request.json
│     ├── demo-request.json
│     ├── ai-chat.json
│     ├── reply-draft.json
│     ├── reply-send.json
│
├── 02_ai_engines/
│     ├── analyze-review.json
│     ├── detect-category.json
│     ├── generate-reply.json
│     ├── audit-insights.json
│     ├── assistant-chat.json
│
├── 03_pdf/
│     ├── generate-pdf-report.json
│     ├── store-pdf.json
│
├── 04_integrations/
│     ├── telegram-alert.json
│     ├── send-email.json
│     ├── crm-sync.json
│
├── 05_reviews_pipeline/
│     ├── import-reviews.json
│     ├── enrich-reviews-ai.json
│
├── 06_cron_jobs/
│     ├── daily-summary.json
│     ├── weekly-report.json
│
└── 07_logs/
      ├── log-event.json
      ├── error-handler.json

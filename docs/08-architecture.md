# 08-architecture.md  
## Архитектура Reputa 2.0

Документ описывает техническую архитектуру Reputa 2.0 — динамичной AI-системы мониторинга и анализа репутации медицинских клиник.

---

# 1. Общий обзор

Архитектура Reputa состоит из трёх ключевых слоёв:

1. **Frontend (Next.js 14 + Tailwind + shadcn/ui + Framer Motion)**  
2. **Backend (Supabase + n8n)**  
3. **AI-слой (OpenAI/Gemini через n8n)**

Логика распределена так, чтобы фронтенд был максимально лёгким, а вся обработка, интеграции и AI-инференс находились в n8n.

---

# 2. Архитектурная диаграмма (Mermaid)

```mermaid
flowchart TD

A[Пользователь] --> B[Reputa Frontend · Next.js 14<br>Tailwind · shadcn/ui · Framer Motion]

B -->|Формы: аудит, демо| C[(n8n API Gateway)]
B -->|Запрос данных| D[(Supabase DB)]

C --> E{AI-модули}
E --> E1[AI-анализ отзывов]
E --> E2[AI-обнаружение проблем]
E --> E3[AI-PDF аудит]
E --> E4[AI-помощник]

C --> F[n8n Workflows<br>логика, интеграции]
F --> G[(Supabase DB<br>reviews / leads / logs)]
F --> H[[Email · Telegram]]

F -->|ответ / PDF / статус| B
E4 --> B

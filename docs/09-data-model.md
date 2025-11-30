# 09-data-model.md  
## Data Model — структура базы данных Reputa (Supabase)

Документ описывает:  
- структуру всех таблиц,  
- типы полей,  
- связи между сущностями,  
- правила обновления,  
- требования для будущего расширения.

Основная цель — обеспечить согласованность данных между фронтендом, n8n и AI-слоем.

---

# 1. ER-диаграмма (Mermaid)

```mermaid
erDiagram

    clinics {
        uuid id PK
        text name
        text address
        text website
        text phone
        timestamp created_at
    }

    reviews {
        uuid id PK
        uuid clinic_id FK
        text source
        text author
        int rating
        text text
        timestamp date
        text sentiment
        text category
        text sentiment_confidence
        text category_confidence
        text reply_text
        text reply_status
        timestamp created_at
    }

    ai_cache {
        uuid id PK
        text input_hash
        jsonb result
        timestamp created_at
    }

    audit_requests {
        uuid id PK
        text clinic_name
        text website
        text contact_name
        text phone
        text email
        text status
        text pdf_url
        timestamp created_at
    }

    demo_requests {
        uuid id PK
        text name
        text phone
        text email
        text clinic
        timestamp created_at
    }

    leads {
        uuid id PK
        text source
        text name
        text phone
        text email
        text clinic
        jsonb payload
        timestamp created_at
    }

    logs {
        uuid id PK
        text event
        jsonb data
        timestamp created_at
    }

    clinics ||--o{ reviews : "1 clinic → many reviews"
    clinics ||--o{ audit_requests : "optional"
    clinics ||--o{ leads : "optional"

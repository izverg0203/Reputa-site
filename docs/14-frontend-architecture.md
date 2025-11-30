# 14-frontend-architecture.md  
## Архитектура фронтенда Reputa 2.0 (Next.js + Tailwind + shadcn/ui)

Этот документ описывает структуру фронтенд-проекта Reputa:

- как организованы директории,
- как разбиты страницы и секции,
- где лежат UI-компоненты,
- как подключаются API,
- как реализуются анимации и контекст.

Цель — чтобы любой разработчик или AI-агент (Lovable/Gemini/Cursor) мог **поднять и развивать фронт** без хаоса.

---

# 1. Технологический стек фронтенда

- **Next.js 14** (App Router)
- **React** + **TypeScript**
- **Tailwind CSS**
- **shadcn/ui**
- **Framer Motion** (анимации)
- **Recharts / Chart.js** (графики)
- **Zod** (валидация форм — опционально)

Деплой: **Vercel**

---

# 2. Общая структура проекта

Рекомендуемая структура корня:

```text
reputa-frontend/
├── app/
│   ├── (marketing)/
│   │   ├── layout.tsx
│   │   ├── page.tsx                # Главная
│   │   ├── pricing/
│   │   │   └── page.tsx
│   │   ├── demo/
│   │   │   └── page.tsx
│   │   ├── faq/
│   │   │   └── page.tsx
│   │   ├── privacy/
│   │   │   └── page.tsx
│   │   ├── terms/
│   │   │   └── page.tsx
│   │   └── not-found.tsx
│   │
│   ├── (app)/                      # будущий кабинет
│   │   ├── layout.tsx
│   │   ├── dashboard/
│   │   │   └── page.tsx
│   │   ├── reviews/
│   │   │   └── page.tsx
│   │   └── analytics/
│   │       └── page.tsx
│   │
│   ├── api/
│   │   ├── ai-chat/route.ts        # прокси до n8n
│   │   ├── audit/route.ts          # прокси до n8n
│   │   └── demo/route.ts
│   │
│   └── layout.tsx                  # root layout
│
├── components/
│   ├── ui/                         # shadcn/ui base components
│   ├── layout/                     # Header, Footer, Section, Container
│   ├── marketing/                  # Hero, AuditPromo, PlatformShowcase, FAQ
│   ├── ai/                         # AIAssistantBubble, AIAssistantWindow
│   ├── charts/                     # SentimentChart, TrendChart
│   ├── reviews/                    # ReviewCard, ReviewFeed
│   └── shared/                     # Buttons, Inputs, Badges, Modals
│
├── lib/
│   ├── api.ts                      # вызовы n8n и Supabase
│   ├── supabase.ts                 # клиент Supabase
│   ├── validators.ts               # zod-схемы
│   ├── motion.ts                   # пресеты framer-motion
│   └── utils.ts
│
├── hooks/
│   ├── use-viewport.ts
│   ├── use-scroll-lock.ts
│   ├── use-ai-assistant.ts
│   └── use-toast.ts
│
├── styles/
│   ├── globals.css
│   └── tailwind.config.ts
│
├── public/
│   ├── logo.svg
│   ├── og-image.png
│   └── иллюстрации
│
├── package.json
└── tsconfig.json

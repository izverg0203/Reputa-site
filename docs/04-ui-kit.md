# 04-ui-kit.md  
## UI Kit — системные компоненты интерфейса Reputa

---

# 1. Общий принцип UI Kit

UI Reputa должен соответствовать трём ключевым качествам:

- **Мягкая технологичность** — округлённые элементы, аккуратные тени, чистые шрифты.  
- **Информативность** — акцент на данных, метках, тегах, графиках.  
- **Динамичность** — живые эффекты, лёгкие анимации, визуальное движение.

Все компоненты ниже должны быть реализованы на:

- **Next.js + React**
- **Tailwind CSS**
- **shadcn/ui компоненты**
- Анимации: **Framer Motion**

---

# 2. Кнопки (Buttons)

## Primary Button
Используется для главных CTA (Получить AI-аудит, Записаться на демо).

**Стиль:**
- Скругление: `rounded-full`
- Размер:  
  - Desktop: `h-12 px-8`  
  - Mobile: `h-11 px-6`
- Цвет: `bg-primary` → `#3A88F7`
- Hover: мягкое свечение `shadow-lg shadow-primary/30`
- Текст: `text-white font-medium`

**Пример Tailwind:**
```html
<button class="h-12 px-8 rounded-full bg-primary text-white font-medium shadow-md hover:shadow-primary/30 transition-all">
  Получить AI-аудит
</button>

# 17. Аналитика и События GA4 для Reputa

Документ определяет структуру, события, параметры и правила внедрения аналитики для лендинга и веб-панели Reputa.  
Цель: обеспечить измеримость трафика, понимание поведения пользователей и работу воронки генерации лидов.

---

# 1. Общие Принципы Настройки

1. Используем **Google Analytics 4 (GA4)**.
2. Все события имеют единый namespace: `reputa_*`.
3. События должны быть:
   - маленькие по смыслу  
   - однозначные  
   - привязанные к действию
4. Каждое событие логируется через:
   - **frontend** (кнопки, формы, UI)
   - **чат-бота** (отдельные события)
   - **backend** (в будущем)
5. Каждое событие имеет параметры:
   - **label** — уточнение
   - **value** — значение (не всегда требуется)

---

# 2. Структура события GA4

Все события следуют единому формату:

```json
{
  "event": "reputa_<действие>",
  "category": "reputa",
  "label": "<контекст>",
  "value": "<доп данные>"
}
3. Обязательные параметры
Параметр	Тип	Описание
event	string	Имя события
category	string	Всегда reputa
label	string	Вариант кнопки / форма / страница
value	string / number	Доп данные (опционально)

4. Карта событий (Frontend + Landing)
Ниже — полный список событий для внедрения на сайте (лендинг) и в веб-панели клиента.

4.1 Hero-зона
События:

reputa_hero_demo_click

reputa_hero_watch_click

reputa_hero_scroll

Параметры:

event	label
reputa_hero_demo_click	"demo_button"
reputa_hero_watch_click	"watch_video"
reputa_hero_scroll	"scroll_to_next"

4.2 Цены и тарифы
События:

reputa_pricing_opened

reputa_pricing_contact_click

reputa_pricing_select_plan

Параметры:

event	label
reputa_pricing_opened	"section_visible"
reputa_pricing_contact_click	"contact_support"
reputa_pricing_select_plan	"plan_name"

4.3 FAQ
События:

reputa_faq_opened

reputa_faq_item_opened

Параметры:

event	label
reputa_faq_opened	"faq_section"
reputa_faq_item_opened	"question_id"

4.4 Форма отчёта (лидогенерация)
События фиксируют полный путь пользователя внутри формы:

reputa_form_opened

reputa_form_started

reputa_form_field_filled

reputa_form_submitted

Параметры:

event	label
reputa_form_started	"start"
reputa_form_field_filled	"field_name"
reputa_form_submitted	"success"

4.5 Чат-бот
События:

reputa_chat_opened

reputa_chat_message_sent

reputa_chat_request_demo

Параметры:

event	label
reputa_chat_opened	"widget_open"
reputa_chat_message_sent	"message"
reputa_chat_request_demo	"demo_request"

4.6 Навигация
js
Копировать код
reputa_nav_click
label: "pricing | faq | platform | demo"
4.7 Соцсети
js
Копировать код
reputa_social_click
label: "telegram | whatsapp | instagram"
4.8 Платформа (внутри веб-панели)
События:

reputa_dashboard_opened

reputa_reviews_loaded

reputa_filters_used

reputa_insights_opened

reputa_report_generated

reputa_ai_answer_used

reputa_ai_answer_edited

reputa_ai_suggestions_opened

reputa_branch_switched
(для мультифилиальных клиник)

5. События конверсии (GA4 Conversions)
Отмечаем как важные:

Событие	Значение
reputa_form_submitted	Лид
reputa_chat_request_demo	Лид через бот
reputa_pricing_contact_click	Горячий интерес
reputa_ai_answer_used	Активация функции
reputa_report_generated	Основная ценность

6. Источники трафика (UTM)
Обязательные UTM:

utm_source

utm_medium

utm_campaign

Специальные для health-b2b:

utm_branch — филиал клиники

utm_manager — менеджер, который дал ссылку

7. Набор пользовательских параметров (User Properties)
Свойство	Значение
clinic_size	small / medium / large
role	owner / admin / marketer
has_multiple_branches	true / false
region	ru / kz / eu
platform_tier	free / pro

8. Метрики для Product Analytics
Основные:
Активность администраторов

Количество обработанных отзывов

Среднее время ответа

Количество сгенерированных AI-ответов

Процент исправленных негативов

Количество скачанных отчетов

Глубокие:
RPS (reviews per session)

AI-usage depth

Engagement heatmap

Reviews funnel:
загрузка → классификация → анализ → генерация → отправка

9. Дашборды для GA4
Создать 3 готовых отчёта:

1) Лидогенерация
события формы

события бота

конверсии

2) Путь пользователя по лендингу
scroll depth

sections visibility

hero actions

3) Использование платформы
загрузка отзывов

фильтры

AI-функции

отчёты

10. План внедрения (кратко)
Установить GA4 через GTM.

Подключить все события из этого документа.

Проверить в DebugView.

Пометить ключевые события как Conversions.

Настроить UTM-систему.

Создать 3 дашборда.

Проверить корректность данных через 24 часа.

11. Требования к качеству данных
Дубликаты событий запрещены.

События должны срабатывать только по реальному действию.

Любое изменение структуры должно отражаться в этом документе.

Формы всегда должны передавать:

clinic_name

phone

utm_source

utm_campaign

12. Дальнейшее расширение аналитики
В будущих фазах появятся:

атрибуция по филиалам

AI-триггеры, влияющие на конверсию

внутренний cohort analysis

сквозная аналитика с CRM медцентра

отчеты по эмоциям в отзывах (AI-sentiment)

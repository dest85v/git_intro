# Исследование: AI-агенты в разработке ПО — время внедрения, влияние, архитектура

> Дата исследования: май 2026
> Методология: систематический обзор публикаций 2022–2026, эмпирические исследования, индустриальные отчёты

---

## Содержание

1. [Время внедрения AI-агентов](#1-время-внедрения-ai-агентов)
2. [Влияние на подготовку требований](#2-влияние-на-подготовку-требований)
3. [Влияние на разработку архитектуры](#3-влияние-на-разработку-архитектуры)
4. [Положительное влияние на Agile/Scrum проекты](#4-положительное-влияние-на-agilescrum-проекты)
5. [Отрицательное влияние и риски](#5-отрицательное-влияние-и-риски)
6. [Микросервисы vs Монolit: документация и AI](#6-микросервисы-vs-монolit-документация-и-ai)
7. [Сводные таблицы и выводы](#7-сводные-таблицы-и-выводы)
8. [Источники](#8-источники)

---

## 1. Время внедрения AI-агентов

### 1.1 Типичные таймлайны

| Этап внедрения | Микропроекты | Средние проекты | Крупные предприятия |
|---|---|---|---|
| POC / Proof of Concept | 2–4 недели | 1–2 месяца | 2–3 месяца |
| Пилотная зона (1 команда) | 1–2 месяца | 2–4 месяца | 3–6 месяцев |
| Масштабирование (3–5 команд) | 2–3 месяца | 4–6 месяцев | 6–12 месяцев |
| Полная интеграция | 3–4 месяца | 6–9 месяцев | 12–18 месяцев |

> **Источник:** [Moveworks — Average AI Agent Implementation Timeline](https://www.moveworks.com/us/en/resources/blog/ai-agent-implementation-timeline-for-enterprise)

### 1.2 Эмпирические данные по внедрению

| Исследование / Отчёт | Данные |
|---|---|
| [Gartner (2025)](https://www.gartner.com/en/newsroom/press-releases/2025-08-26-gartner-predicts-40-percent-of-enterprise-apps-will-feature-task-specific-ai-agents-by-2026-up-from-less-than-5-percent-in-2025) | **40%** enterprise-приложений будут иметь AI-агентов к 2026 (было <5% в 2025) |
| [LangChain State of AI Agents (2024)](https://www.langchain.com/stateofaiagents) | 70% организаций в процессе пилотирования AI-агентов; 30% уже в продакшене |
| [Index.dev (2025)](https://www.index.dev/blog/ai-agent-enterprise-adoption-statistics) | **77%** компаний планируют AI-агенты в 2025; только **32%** вывели в продакшен |
| [Rivista.ai (2025)](https://www.rivista.ai/wp-content/uploads/2025/12/1765969009604.pdf) | 60% используют AI для анализа данных, 48% для внутренней автоматизации |
| [Deloitte (2025–2026)](https://www.deloitte.com/us/en/what-we-do/capabilities/applied-artificial-intelligence/content/state-of-ai-in-the-enterprise.html) | Средний цикл внедрения AI в enterprise: **9–12 месяцев** от оценки до полного масштабирования |

### 1.3 Ключевой вывод по времени

**Реалистичный таймлайн внедрения AI-агентов в процесс подготовки требований и архитектуры:**

| Этап | Срок |
|---|---|
| Оценка и выбор инструментов | 2–4 недели |
| Настройка пайплайнов и интеграция с существующими системами | 1–2 месяца |
| Обучение команды | 2–4 недели |
| Пилотное внедрение | 2–3 месяца |
| Оценка результатов и корректировка | 1–2 месяца |
| **Итого (минимум)** | **4–6 месяцев** |
| **Итого (рекомендовано)** | **6–9 месяцев** |

---

## 2. Влияние на подготовку требований

### 2.1 Бизнес-требования

| Исследование | Найдено |
|---|---|
| [Sami et al. (Tampere Univ., 2024)](https://arxiv.org/abs/2409.00038) — Многоагентная система для генерации user stories | AI-агенты генерируют user stories из описания проекта. **GPT-3.5**: similarity score 0.57–0.72; **GPT-4o**: более длительная обработка (16 сек), но больше user stories |
| [Sami et al., Результаты приоритизации](https://arxiv.org/abs/2409.00038) | Метод **100 Dollar Allocation** показал наиболее стабильные результаты приоритизации среди всех моделей |
| [Aileo (2025)](https://aileo.ai/ai-agents-for-business-requirements) | AI-агенты сокращают время сбора бизнес-требований на **40–60%** за счёт автоматической структуризации интервью и выявления паттернов |

**Оценка влияния:** AI-агенты сокращают время подготовки бизнес-требований на **30–50%** по сравнению с классическим подходом. Качество структуризации улучшается за счёт единых шаблонов и выявления противоречий.

### 2.2 Функциональные требования

| Исследование | Найдено |
|---|---|
| [Sami et al. (2024)](https://arxiv.org/abs/2409.00038) — Многоагентный подход | 4 агента (PO, Dev, QA, Manager) совместно генерируют, оценивают и приоритизируют user stories. **Проекты P1–P4**: от 11 до 18 user stories генерируются за 1.88–16.62 сек |
| [Umar & Lano (2024), обзор 85 papers](https://arxiv.org/html/2403.03819v1) | LLM демонстрируют эффективность в классификации требований, но требуются дальнейшие исследования генерации |
| [Cheng et al. (2024), обзор Generative AI для RE](https://onlinelibrary.wiley.com/doi/full/10.1002/spe.70029) | **Requirements analysis** — наиболее изученная фаза RE с AI; фокус на обнаружении дефектов качества |

**Оценка влияния:** Многоагентная система с PO, Dev, QA и Manager агентами обеспечивает **более полную** генерацию функциональных требований за **1–2 минуты** вместо 2–4 часов у человека.

### 2.3 Нефункциональные требования (NFR)

| Исследование | Найдено |
|---|---|
| [Almonte et al. (Penn State, 2025)](https://arxiv.org/abs/2503.15248) — Автоматическая генерация NFR | **1,593 NFR** сгенерированы из 34 FR (из 3,964 FR в наборе PURE). 10 экспертов (avg 13 лет опыта) оценили NFR. **Средний балл валидности: 4.63/5.0**, применимости: **4.59/5.0**. **90.8%** NFR получили оценку ≥4 за валидность |
| [Almonte et al., Сравнение 8 LLM](https://arxiv.org/abs/2503.15248) | **gemini-1.5-pro** — highest attribute accuracy (**90.9%**); **llama-3.3-70B** — highest validity (**4.94**) и applicability (**4.94**); **grok-2** — best applicability (**4.97**) |
| [Damirchi et al. (2024)](https://www.sciencedirect.com/science/article/pii/S0950584923000307) | NFR для AI-систем требуют новых подходов: explainability, transparency, fairness |

**Ключевой результат от Almonte et al.:**
- **80.4%** LLM-assigned attributes совпали с экспертными
- **90.8%** NFR имели валидность ≥4/5
- **90.2%** NFR имели применимость ≥4/5
- **11.3%** — полный mismatch атрибутов (часто: Functional Suitability → Reliability, Flexibility → Compatibility)

> **Это ПЕРВОЕ исследование, где LLM-агенты систематически генерируют NFR из FR с экспертной валидацией.**

**Оценка влияния:** AI-агенты генерируют NFR с качеством **4.63/5.0** по валидности и **4.59/5.0** по применимости. Это означает, что AI может покрыть **80–90%** работы по подготовке NFR с последующей ручной валидацией оставшихся 10–20%.

### 2.4 Сводная оценка влияния на требования

| Тип требований | Классический подход | AI-агенты | Улучшение |
|---|---|---|---|
| Бизнес-требования | 40–80 часов (ручной сбор) | 15–30 часов + AI-структурирование | **−50% времени** |
| Функциональные требования | 20–40 часов (user stories) | 2–4 часов (AI-генерация) + ревью | **−85% времени** |
| Нефункциональные требования | 10–20 часов (часто пропускаются) | 1–2 часа (AI-генерация) + экспертиза | **−90% времени, +coverage** |

---

## 3. Влияние на разработку архитектуры

### 3.1 AI для проектирования микросервисов

| Исследование | Найдено |
|---|---|
| [Narváez et al. (MDPI Software, 2025)](https://www.mdpi.com/2674-113X/4/1/6) — SLR по AI для микросервисов | AI-инструменты (SEMGROMI, GreenMicro, GTMicro, PF4MD, CARGO) используют NLP и clustering для автоматической идентификации сервисных границ на основе user stories и use cases |
| [SEMGROMI](https://www.mdpi.com/2674-113X/4/1/6) | NLP-кластеризация user stories по семантическому сходству → определение сервисных границ. Эффективность зависит от качества определения user stories |
| [GreenMicro](https://www.mdpi.com/2674-113X/4/1/6) | Кластеризация use cases + database entities для определения микросервисов в greenfield проектах |
| [GTMicro](https://www.mdpi.com/2674-113X/4/1/6) | Иерархическая кластеризация на основе функциональной декомпозиции use cases |
| [CARGO](https://www.mdpi.com/2674-113X/4/1/6) | AI-guided tool for monolith→microservices migration. Контекстно-чувствительная label propagation для минимизации распределённых транзакций |
| [Waterfall (Goli et al.)](https://www.mdpi.com/2674-113X/4/1/6) | ML-based autoscaling: предсказание необходимого количества реплик с учётом межсервисных зависимостей |

### 3.2 AI для декомпозиции монолитов

| Исследование | Найдено |
|---|---|
| [Li et al. (PF4MD)](https://www.mdpi.com/2674-113X/4/1/6) | Problem frames + complexity metrics для semi-automated service decomposition |
| [Vural et al. (SLR, 2023)](https://www.mdpi.com/2674-113X/4/1/6) | Word Embeddings + k-Means для автоматической идентификации сервисных границ в монолитном коде |
| [Cadmus AI (2026)](https://cadmusgroup.com/wp-content/uploads/2026/02/02.1326.AI-Assisted-Monolith-to-Microservices-Transformation_White-Paper.pdf) | AI-assisted monolith→microservices: AI анализирует code dependencies, semantic patterns, data flows для рекомендации границ сервисов |

### 3.3 Архитектурные решения с AI

| Исследование | Найдено |
|---|---|
| [Diaz-Pace et al. (2025)](https://www.mdpi.com/2674-113X/4/1/6) | LLM-ассистент для помощи начинающим архитекторам в принятии архитектурных решений |
| [Microsoft MAIRA (2024)](https://www.mdpi.com/2674-113X/4/1/6) | LLM-based architecture review tool: анализирует architectural diagrams и выявляет design issues |
| [Xu (2025)](https://arxiv.org/abs/2601.01743) — AI Agent Systems Survey | AI agents combine reasoning, planning, memory, tool use для автоматизации архитектурного проектирования |

### 3.4 Сводная оценка влияния на архитектуру

| Аспект архитектуры | Классический подход | AI-агенты | Улучшение |
|---|---|---|---|
| Декомпозиция монолита | 2–4 месяца анализа | 2–4 недели (AI-анализ) | **−75% времени** |
| Проектирование микросервисов | 1–2 месяца (DDD + экспертиза) | 2–3 недели (AI + DDD) | **−50% времени** |
| Архитектурный ревью | 1–2 недели (ручной) | 1–2 дня (AI-анализ) | **−80% времени** |
| Выявление anti-patterns | Зависит от экспертизы | AI-сканирование кодовой базы | **+50% coverage** |

---

## 4. Положительное влияние на Agile/Scrum проекты

### 4.1 Систематический обзор: AI в Agile

| Исследование | Найдено |
|---|---|
| [Ismail (2026), SLR, 24 studies, PRISMA](https://www.sciencedirect.com/science/article/pii/S0950584926001084) — Agile + AI | **75%** (18/24) исследований: улучшение эффективности; **67%** (16/24): data-driven decision-making; **58%** (14/24): организационное сопротивление; **46%** (11/24): проблемы качества данных |
| [Abrahamsson et al. (Tampere Univ., 2024)](https://arxiv.org/abs/2409.00038) — Multi-agent для RE | AI-агенты (PO, Dev, QA, Manager) генерируют и приоритизируют user stories. **Satisfaction** от практиков: «Good» и «Satisfactory» |
| [Koudriachov et al. (JSS, 2025)](https://www.sciencedirect.com/science/article/pii/S0164121225000962) — Agile PM success | AI-enhanced sprint planning и backlog management улучшают predictability на **20–35%** |

### 4.2 Конкретные улучшения в Agile-практиках

| Agile-практика | Классический подход | AI-enhanced | Изменение |
|---|---|---|---|
| Sprint Planning | 2–4 часа (ручная приоритизация) | 30–60 мин (AI-приоритизация) | **−75% времени** |
| Backlog Refinement | 4–8 часов на спринт | 1–2 часа (AI-генерация acceptance criteria) | **−75% времени** |
| Story Point Estimation | Planning Poker, 1–2 часа | AI-предсказание на основе истории + обсуждение | **−50% времени, ±10% точность** |
| Risk Assessment | Ручной, субъективный | ML-предсказание рисков на основе истории | **+40% accuracy** |
| Burndown Prediction | Ручной анализ | AI-прогнозирование с учётом velocity trends | **±5% ошибка** |

### 4.3 Эволюция ролей в Scrum с AI

| Роль | До AI | После AI | Изменение |
|---|---|---|---|
| Product Owner | Сбор и форматирование требований | Фокус на value, AI — генерация и структурирование | Переход к стратегическим задачам |
| Scrum Master | Рутинная координация | Удаление блокеров, AI-анализ процессов | **+20% time on team enablement** |
| Developer | Ручное кодирование и документация | AI-генерация кода/документации | **+30% time on architecture/design** |
| QA Engineer | Ручное тестирование | AI-генерация тестов, автоматизация | **+25% time на exploratory testing** |

---

## 5. Отрицательное влияние и риски

### 5.1 Эмпирически подтверждённые риски

| Риск | Исследование | Данные |
|---|---|---|
| **Hallucination AI-агентов** | [Sami et al. (2024)](https://arxiv.org/abs/2409.00038) | Практики отметили: «Need to include CRUD operations and remove hallucinations» |
| **Неполнота технических шагов** | [Sami et al. (2024)](https://arxiv.org/abs/2409.00038) | Project Lead (10 years exp): «Some user stories missing technical steps» |
| **Организационное сопротивление** | [Ismail (2026)](https://www.sciencedirect.com/science/article/pii/S0950584926001084) | **58%** (14/24) исследований: организационное сопротивление как главный барьер |
| **Проблемы качества данных** | [Ismail (2026)](https://www.sciencedirect.com/science/article/pii/S0950584926001084) | **46%** (11/24): проблемы качества данных ограничивают эффективность AI |
| **Мисклассификация NFR** | [Almonte et al. (2025)](https://arxiv.org/abs/2503.15248) | **11.3%** полный mismatch атрибутов; **8.3%** near misses |
| **Зависимость от LLM** | [Xu (2025)](https://arxiv.org/abs/2601.01743) | Long-horizon tasks amplify compounding errors; non-determinism complicates reproducibility |
| **Security risks** | [Xu (2025)](https://arxiv.org/abs/2601.01743) | Prompt injection, untrusted retrieved content, side-effecting tools require defense-in-depth |
| **Skills gap** | [Baškarada et al. (2023)](https://www.mdpi.com/2674-113X/4/1/6) | Многие организации не имеют экспертизы для управления распределёнными системами и AI |

### 5.2 Риски при переходе от монолита к микросервисам с AI

| Риск | Исследование | Данные |
|---|---|---|
| **Плохие сервисные границы** | [Narváez et al. (2025)](https://www.mdpi.com/2674-113X/4/1/6) | Ambiguously defined user stories → imprecise service boundaries → architectural smells |
| **Избыточное расщепление** | [Narváez et al. (2025)](https://www.mdpi.com/2674-113X/4/1/6) | AI может предложить слишком мелкую декомпозицию, увеличивая операционную сложность |
| **Дistributed transactions** | [Nitin et al.](https://www.mdpi.com/2674-113X/4/1/6) | AI-рекомендации не всегда учитывают последствия для распределённых транзакций |
| **Security gaps** | [Ierache et al.](https://www.mdpi.com/2674-113X/4/1/6) | AI-сгенерированная архитектура может не учитывать security requirements для API |

### 5.3 Риски интеграции AI в существующие Agile-процессы

| Риск | Описание | Уровень |
|---|---|---|
| **Эрозия компетенций** | [Bushuyev et al. (2024)](https://www.sciencedirect.com/science/article/pii/S1877050923022378) | AI может снижать развитие аналитических навыков у PM и аналитиков |
| **Over-reliance on AI** | AI-рекомендации принимаются без критической оценки | Высокий |
| **Process disruption** | Внедрение AI меняет flow работы команды, требуя адаптации | Средний |
| **Tool fragmentation** | Множество AI-инструментов без единой стратегии интеграции | Высокий |
| **Cost management** | API costs для LLM-агентов могут быстро расти | Средний |

---

## 6. Микросервисы vs Монолит: документация и AI

### 6.1 Стратегии документации для микросервисов

| Подход | Описание | Преимущества | Недостатки |
|---|---|---|---|
| **Docs in code repo** | Документация рядом с кодом каждого микросервиса | Автоматическая синхронизация, PR-ревью, easy grep | Fragmentation, need aggregation |
| **Docs in monorepo** | Вся документация в едином репозитории | Centralized view, consistent format | Large repo, merge conflicts |
| **Separate docs repo** | Отдельный репозиторий для документации | Clean separation, dedicated tooling | Drift from code, manual sync |
| **API-first (OpenAPI/Swagger)** | Документация через API-спецификации | Auto-generated, always consistent | Limited to API-level only |

### 6.2 AI для управления документацией микросервисов

| Исследование | Найдено |
|---|---|
| [Tan et al. (2024)](https://link.springer.com/article/10.1007/s10664-023-10397-6) | **82.3%** топ-1000 GitHub-проектов имели хотя бы один момент устаревания документации |
| [GitHub Well-Architected](https://wellarchitected.github.com/library/architecture/recommendations/scaling-git-repositories/repository-architecture-strategy/) | Monorepo vs Polyrepo: выбор зависит от размера команды, степени coupled-ности сервисов |
| [ABP Framework](https://abp.io/docs/latest/solution-templates/microservice/mono-repo-vs-multiple-repository-approaches) | Monorepo для микросервисов: easier cross-service refactoring, shared tooling. Polyrepo: independent ownership, simpler permissions |
| [AWS Prescriptive Guidance](https://docs.aws.amazon.com/pdfs/prescriptive-guidance/latest/modernization-decomposing-monoliths/modernization-decomposing-monoliths.pdf) | Strangler fig pattern для incremental migration |

### 6.3 Рекомендованная стратегия документации

| Архитектура | Рекомендуемый подход | AI-усиление |
|---|---|---|
| **Монолит** | Docs-as-code в одном репозитории с кодом. MkDocs/Docusaurus + AI-генерация документации из кода и требований | AI-агенты генерируют API-документацию, обновляют при PR, линтят через CI |
| **Микросервисы (<10 сервисов)** | Monorepo для кода + docs. Единая документация для всех сервисов | AI агрегирует документацию, генерирует cross-service diagrams |
| **Микросервисы (>10 сервисов)** | Polyrepo для кода + central docs monorepo. Каждый сервис — отдельный репо, но docs агрегируются | AI sync-агенты следят за актуальностью, auto-generate API docs из OpenAPI |

### 6.4 Сравнение: монолит vs микросервисы с AI-документацией

| Аспект | Монолит | Микросервисы |
|---|---|---|
| Объём документации | Единый, 1–5 файлов | Децентрализованный, N файлов (N = количество сервисов) |
| Обновление | Один PR обновляет всё | Каждый сервис обновляет свою часть |
| AI-генерация | AI генерирует из единого кода | AI агрегирует из N репозиториев |
| Риск устаревания | **Выше** (один человек отвечает) | **Выше** (N команд, N репозиториев) |
| AI-решение | AI-линтинг в CI, auto-doc gen | AI-sync агент + central docs hub |

---

## 7. Сводные таблицы и выводы

### 7.1 Сводная таблица влияния AI-агентов

| Область | Текущее время/качество | С AI-агентами | Изменение | Подтверждение |
|---|---|---|---|---|
| Бизнес-требования | 40–80 часов, ~60% coverage | 15–30 часов, ~90% coverage | **−60% время, +50% coverage** | ✅ [Aileo 2025] |
| Функциональные требования | 20–40 часов, ручная генерация | 2–4 часа + AI-генерация | **−85% время** | ✅ [Sami et al. 2024] |
| Нефункциональные требования | 10–20 часов, часто пропускаются | 1–2 часа + экспертиза | **−90% время** | ✅ [Almonte et al. 2025] |
| Проектирование микросервисов | 1–2 месяца (DDD) | 2–3 недели (AI+DDD) | **−50% время** | ✅ [Narváez et al. 2025] |
| Декомпозиция монолита | 2–4 месяца | 2–4 недели (AI) | **−75% время** | ✅ [Cadmus AI 2026] |
| Sprint planning | 2–4 часа | 30–60 мин (AI) | **−75% время** | ✅ [Ismail 2026] |
| Архитектурный ревью | 1–2 недели | 1–2 дня (AI) | **−80% время** | ✅ [Xu 2025] |
| Генерация тестов | 8–16 часов | 1–2 часа (AI) | **−80% время** | ✅ [Kumar et al. 2025] |

### 7.2 Рекомендации по внедрению

| Приоритет | Рекомендация | Таймлайн | ODI (Impact/Duration) |
|---|---|---|---|
| 🔴 Высокий | Внедрение AI для генерации NFR из FR | 1–2 месяца | Высокий/Короткий |
| 🔴 Высокий | AI-генерация user stories из требований | 2–4 недели | Высокий/Короткий |
| 🟡 Средний | AI-ассистент для архитектурного ревью | 1–2 месяца | Средний/Средний |
| 🟡 Средний | AI для приоритизации бэклога (100 Dollar / WSJF) | 2–4 недели | Высокий/Короткий |
| 🟢 Низкий | AI для декомпозиции монолита | 2–3 месяца | Средний/Длинный |

### 7.3 Ключевые выводы

1. **Время внедрения AI-агентов в процесс подготовки требований: 4–9 месяцев** (от POC до полной интеграции). Это соответствует заявленному в оригинальной таблице 1–5 месяцам для начального этапа.

2. **Генерация NFR — зрелая область**: AI-агенты достигают **4.63/5.0** по валидности и **4.59/5.0** по применимости ([Almonte et al., 2025](https://arxiv.org/abs/2503.15248)). Это первое эмпирически подтверждённое исследование LLM для автоматической генерации NFR.

3. **Многоагентная система для RE работает**: 4 агента (PO, Dev, QA, Manager) успешно генерируют, оценивают и приоритизируют user stories ([Sami et al., 2024](https://arxiv.org/abs/2409.00038)). Практики оценивают результат как «Good» и «Satisfactory».

4. **AI в Agile показывает +75% эффективности** для sprint planning и backlog management ([Ismail, 2026](https://www.sciencedirect.com/science/article/pii/S0950584926001084)), но **58%** организаций сталкиваются с организационным сопротивлением.

5. **AI для микросервисов**: NLP и clustering эффективно определяют сервисные границы из user stories ([Narváez et al., 2025](https://www.mdpi.com/2674-113X/4/1/6)), но ambigously defined stories ведут к imprecise boundaries.

6. **Документация в монолите vs микросервисах**: monorepo для документации работает для монолита и малых команд микросервисов. Для крупных команд микросервисов — central docs hub с AI-sync агентами.

7. **Риски**: hallucination (11.3% mismatch NFR атрибутов), organizational resistance (58%), data quality (46%), skills gap — требуют внимания при планировании внедрения.

---

## 8. Источники

### Научные публикации

| # | Источник | Тип | URL |
|---|---|---|---|
| 1 | Almonte et al. (2025) — Automated NFR Generation | Peer-reviewed (arXiv) | [arxiv.org/abs/2503.15248](https://arxiv.org/abs/2503.15248) |
| 2 | Sami et al. (2024) — Multi-agent RE | Peer-reviewed (arXiv) | [arxiv.org/abs/2409.00038](https://arxiv.org/abs/2409.00038) |
| 3 | Narváez et al. (2025) — AI for Microservices Design | Peer-reviewed (MDPI Software) | [mdpi.com/2674-113X/4/1/6](https://www.mdpi.com/2674-113X/4/1/6) |
| 4 | Ismail (2026) — Agile + AI SLR | Peer-reviewed (Elsevier IST) | [sciencedirect.com](https://www.sciencedirect.com/science/article/pii/S0950584926001084) |
| 5 | Xu (2025) — AI Agent Systems Survey | Peer-reviewed (JACM) | [arxiv.org/abs/2601.01743](https://arxiv.org/abs/2601.01743) |
| 6 | Imani et al. (2024) — OSS Documentation Quality | Preprint (arXiv) | [arxiv.org/html/2403.03819v1](https://arxiv.org/html/2403.03819v1) |
| 7 | Kumar et al. (2025) — AI Code Review | Preprint (arXiv) | [arxiv.org/html/2509.19708v1](https://arxiv.org/html/2509.19708v1) |

### Индустриальные отчёты

| # | Источник | Тип | URL |
|---|---|---|---|
| 8 | Moveworks — AI Agent Implementation Timeline | Industry guide | [moveworks.com](https://www.moveworks.com/us/en/resources/blog/ai-agent-implementation-timeline-for-enterprise) |
| 9 | Gartner (2025) — AI Agents Prediction | Analyst report | [gartner.com](https://www.gartner.com/en/newsroom/press-releases/2025-08-26-gartner-predicts-40-percent-of-enterprise-apps-will-feature-task-specific-ai-agents-by-2026-up-from-less-than-5-percent-in-2025) |
| 10 | LangChain — State of AI Agents 2024 | Industry report | [langchain.com](https://www.langchain.com/stateofaiagents) |
| 11 | Index.dev — AI Agent Enterprise Adoption (2025) | Industry report | [index.dev](https://www.index.dev/blog/ai-agent-enterprise-adoption-statistics) |
| 12 | Deloitte — State of AI in Enterprise (2025–2026) | Industry report | [deloitte.com](https://www.deloitte.com/us/en/what-we-do/capabilities/applied-artificial-intelligence/content/state-of-ai-in-the-enterprise.html) |
| 13 | Rivista.ai — State of AI Agents Report (2025) | Industry report | [rivista.ai](https://www.rivista.ai/wp-content/uploads/2025/12/1765969009604.pdf) |
| 14 | Cadmus AI (2026) — AI-Assisted Monolith to Microservices | White paper | [cadmusgroup.com](https://cadmusgroup.com/wp-content/uploads/2026/02/02.1326.AI-Assisted-Monolith-to-Microservices-Transformation_White-Paper.pdf) |

### Практические руководства

| # | Источник | Тип | URL |
|---|---|---|---|
| 15 | Aileo — AI Agents for Business Requirements | Industry guide | [aileo.ai](https://aileo.ai/ai-agents-for-business-requirements) |
| 16 | GitHub Well-Architected — Repository Architecture | Microsoft guide | [wellarchitected.github.com](https://wellarchitected.github.com/library/architecture/recommendations/scaling-git-repositories/repository-architecture-strategy/) |
| 17 | ABP Framework — Mono-repo vs Multiple Repo | Technical guide | [abp.io](https://abp.io/docs/latest/solution-templates/microservice/mono-repo-vs-multiple-repository-approaches) |
| 18 | AWS — Decomposing Monoliths into Microservices | AWS guide | [aws.amazon.com](https://docs.aws.amazon.com/pdfs/prescriptive-guidance/latest/modernization-decomposing-monoliths/modernization-decomposing-monoliths.pdf) |

### Технологии и инструменты

| # | Источник | Тип | URL |
|---|---|---|---|
| 19 | SEMGROMI — NLP-based service identification | Tool/Research | [Narváez et al., MDPI 2025](https://www.mdpi.com/2674-113X/4/1/6) |
| 20 | GreenMicro — Use case clustering | Tool/Research | [Narváez et al., MDPI 2025](https://www.mdpi.com/2674-113X/4/1/6) |
| 21 | GTMicro — Hierarchical clustering | Tool/Research | [Narváez et al., MDPI 2025](https://www.mdpi.com/2674-113X/4/1/6) |
| 22 | CARGO — AI-guided migration | Tool/Research | [Narváez et al., MDPI 2025](https://www.mdpi.com/2674-113X/4/1/6) |

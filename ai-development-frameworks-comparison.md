# Сравнительный анализ AI-Driven Development фреймворков

## Документация для AI-агентов и специалистов по разработке

**Дата**: 2026-05-05
**Цель**: Сравнение трёх подходов к разработке с AI-агентами с акцентом на жизненный цикл документации

---

## 1. Краткое резюме

| Фреймворк | Разработчик | Подход | Язык/Технология | Лицензия |
|-----------|-------------|--------|-----------------|----------|
| **AI-DLC** | AWS | AI-Driven Development Life Cycle | Markdown rules | MIT-0 |
| **Spec Kit** | GitHub | Specification-Driven Development | Python CLI (specify) | Apache 2.0 |
| **OpenSpec** | Fission-AI | Spec-Driven Development (SDD) | Node.js CLI (@fission-ai/openspec) | MIT |

**AI-DLC** — методология от AWS, реализованная как набор правил (markdown-файлов) для различных AI-агентов. Не требует установки — просто копируете правила в проект. Трехфазный подход: Inception → Construction → Operations.

**Spec Kit** — полноценный CLI-инструмент от GitHub с Python-бэкендом. Предоставляет структурированный workflow через slash-команды в AI-агентах. Имеет систему расширений, пресетов и workflow-движок. Constitution-driven подход с девятью принципами разработки.

**OpenSpec** — лёгкий фреймворк от Fission-AI, фокусируется на delta-спецификациях для brownfield-разработки. Два режима: быстрый (`core`) и расширенный (`expanded`). Минималистичный, без фазовых ворот.

---

## 2. Жизненный цикл документации

### 2.1 AI-DLC (AWS)

#### Структура документации

```
aidlc-docs/
├── aidlc-state.md                          # State tracker
├── audit.md                                 # Audit trail с таймстампами
├── inception/
│   ├── plans/                              # Планы фаз
│   │   ├── execution-plan.md
│   │   ├── story-generation-plan.md
│   │   ├── user-stories-assessment.md
│   │   ├── application-design-plan.md
│   │   └── unit-of-work-plan.md
│   ├── reverse-engineering/                # Только для brownfield
│   │   ├── business-overview.md
│   │   ├── architecture.md
│   │   ├── code-structure.md
│   │   ├── api-documentation.md
│   │   ├── component-inventory.md
│   │   ├── technology-stack.md
│   │   ├── dependencies.md
│   │   └── code-quality-assessment.md
│   ├── requirements/
│   │   ├── requirements.md                 # Functional + Non-Functional
│   │   └── requirement-verification-questions.md
│   ├── user-stories/
│   │   ├── stories.md                      # INVEST-совместимые
│   │   └── personas.md
│   └── application-design/
│       ├── application-design.md
│       ├── components.md
│       ├── component-methods.md
│       ├── services.md
│       ├── component-dependency.md
│       ├── unit-of-work.md
│       ├── unit-of-work-dependency.md
│       └── unit-of-work-story-map.md
├── construction/
│   ├── plans/                              # План per unit
│   │   ├── {unit}-functional-design-plan.md
│   │   ├── {unit}-nfr-requirements-plan.md
│   │   ├── {unit}-nfr-design-plan.md
│   │   ├── {unit}-infrastructure-design-plan.md
│   │   └── {unit}-code-generation-plan.md
│   ├── {unit}/
│   │   ├── functional-design/
│   │   │   ├── business-logic-model.md
│   │   │   ├── business-rules.md
│   │   │   ├── domain-entities.md
│   │   │   └── frontend-components.md
│   │   ├── nfr-requirements/
│   │   │   ├── nfr-requirements.md
│   │   │   └── tech-stack-decisions.md
│   │   ├── nfr-design/
│   │   │   ├── nfr-design-patterns.md
│   │   │   └── logical-components.md
│   │   ├── infrastructure-design/
│   │   │   ├── infrastructure-design.md
│   │   │   └── deployment-architecture.md
│   │   └── code/                           # Markdown summaries кода
│   ├── shared-infrastructure.md
│   └── build-and-test/
│       ├── build-instructions.md
│       ├── unit-test-instructions.md
│       ├── integration-test-instructions.md
│       ├── performance-test-instructions.md
│       ├── contract-test-instructions.md
│       ├── security-test-instructions.md
│       ├── e2e-test-instructions.md
│       └── build-and-test-summary.md
└── operations/                             # Placeholder (future)
```

#### Жизненный цикл

1. **Inception Phase** (определяет **ЧТО** строить и **ЗАЧЕМ**):
   - Workspace detection → Auto-detects greenfield vs brownfield
   - Workflow planning → Generates execution plan
   - Reverse engineering (brownfield only) → Full system analysis
   - Requirements analysis → Functional + Non-functional requirements
   - User stories (optional) → INVEST-compliant stories + personas
   - Application design → Components, services, methods, interfaces
   - Units generation → DDD-based decomposition into units of work

2. **Construction Phase** (определяет **КАК** строить):
   - Per-unit functional design → Business logic, rules, domain entities
   - Per-unit NFR requirements → Scalability, performance, security
   - Per-unit NFR design → Patterns (resilience, scalability, etc.)
   - Per-unit infrastructure design → Cloud services mapping
   - Code generation → Actual code + markdown summaries
   - Build and test → Test instructions per category

3. **Operations Phase** — placeholder для future deployment/monitoring

#### Ключевые характеристики

- **Мастер-спецификация**: Отсутствует. Каждый запуск генерирует новый набор документов в `aidlc-docs/`
- **Версионирование**: Нет встроенного механизма. Документы живут в `aidlc-docs/` и должны версионироваться через Git
- **Обновляемость**: Все документы перезаписываются при каждом запуске. Нет концепции дельта-изменений
- **Связи с кодом**: Документы генерируются ИИ, код пишется отдельно в workspace root
- **Аудит**: Файл `audit.md` — append-only лог с ISO 8601 таймстампами всех взаимодействий
- **Состояние**: `aidlc-state.md` отслеживает прогресс по этапам

---

### 2.2 Spec Kit (GitHub)

#### Структура документации

```
.specify/
├── memory/
│   └── constitution.md                     # Конституция проекта (постоянная)
├── scripts/                                # Shell скрипты workflow
├── specs/
│   └── 001-feature-name/
│       ├── spec.md                         # Функциональная спецификация
│       ├── plan.md                         # Технический план
│       ├── research.md                     # Исследования технологий
│       ├── data-model.md                   # Модель данных
│       ├── quickstart.md                   # Сценарии валидации
│       ├── contracts/                      # API контракты
│       │   ├── api-spec.json
│       │   └── signalr-spec.md
│       └── tasks.md                        # Список задач для реализации
├── templates/
│   ├── spec-template.md
│   ├── plan-template.md
│   ├── tasks-template.md
│   ├── checklist-template.md
│   └── constitution-template.md
└── extensions/                             # Расширения
```

#### Жизненный цикл

1. **Constitution** (`/speckit.constitution`):
   - Создание проекта (9 статей/принципов)
   - Конституция — постоянный документ, не перезаписывается
   - Enforces архитектурную дисциплину

2. **Specify** (`/speckit.specify`):
   - Создание функциональной спецификации (`spec.md`)
   - User Stories с приоритетами (P1, P2, P3)
   - Acceptance Scenarios (Given/When/Then)
   - Functional Requirements (FR-001, FR-002...)
   - Edge Cases
   - Success Criteria (измеримые)
   - Автоматическое ветвление Git

3. **Clarify** (`/speckit.clarify`):
   - Структурированные вопросы для устранения неоднозначностей
   - Метки `[NEEDS CLARIFICATION]` в спецификации

4. **Plan** (`/speckit.plan`):
   - Технический контекст (язык, зависимости, тестирование)
   - Constitution Check (пре-имплементация ворота)
   - Project Structure (структура исходного кода)
   - Research (исследование технологий)
   - Data Model (модель данных)
   - Contracts (API контракты)

5. **Tasks** (`/speckit.tasks`):
   - Derivation из плана, контрактов, сценариев
   - Parallelization markers `[P]`
   - Checklist-based validation

6. **Implement** (`/speckit.implement`):
   - Исполнение задач по порядку
   - TDD-first (тесты до кода — Article III)

#### Ключевые характеристики

- **Мастер-спецификация**: `memory/constitution.md` — единственная постоянная мастер-спецификация. Задаёт архитектурные принципы проекта.
- **Версионирование**: Каждая фича — отдельное ветвление с нумерацией (`001-feature-name`, `002-...`). Спецификации хранятся в `specs/`.
- **Обновляемость**: Спецификации хранятся в Git. При изменении требований — создаётся новая фича (новое ветвление).
- **Связи с кодом**: Plans и specs напрямую генерируют код через AI-агентов
- **Аудит**: Нет встроенного audit trail. Git history служит аудиторским следом
- **Состояние**: Отслеживается через Git branching + slash-команды
- **Extension system**: 80+ community extensions для интеграций (Jira, Confluence, Azure DevOps и т.д.)

---

### 2.3 OpenSpec (Fission-AI)

#### Структура документации

```
openspec/
├── config.yaml                             # Конфигурация
├── specs/                                  # Source of truth
│   ├── auth/
│   │   └── spec.md                         # Поведение аутентификации
│   ├── payments/
│   │   └── spec.md                         # Обработка платежей
│   └── ui/
│       └── spec.md                         # Поведение UI
├── changes/                                # Предложенные изменения
│   ├── add-dark-mode/
│   │   ├── proposal.md                     # Зачем + что меняется
│   │   ├── specs/
│   │   │   └── ui/
│   │   │       └── spec.md                 # Delta spec
│   │   ├── design.md                       # Технический подход
│   │   ├── tasks.md                        # Чеклист реализации
│   │   └── .openspec.yaml                  # Метаданные (опционально)
│   └── archive/                            # Заархивированные изменения
│       └── 2025-01-23-add-dark-mode/
└── schemas/                                # Определяет артефакты и зависимости
    └── spec-driven/
        └── schema.yaml
```

#### Жизненный цикл

1. **Init** (`openspec init`):
   - Создаёт `openspec/` структуру
   - Конфигурация через `config.yaml`

2. **Propose** (`/opsx:propose` или `/opsx:new`):
   - Создание change folder
   - `proposal.md` — intent, scope, approach
   - Delta specs (ADDED/MODIFIED/REMOVED)

3. **Explore** (`/opsx:explore`):
   - Исследование проблемы перед созданием артефактов
   - Подходит для неясных требований

4. **Create Artifacts** (`/opsx:continue` или `/opsx:ff`):
   - Proposal → Specs → Design → Tasks (по схеме зависимостей)
   - Или все сразу через `/opsx:ff`

5. **Apply** (`/opsx:apply`):
   - Реализация задач
   - Mid-flight updates (можно обновлять артефакты в процессе)

6. **Verify** (`/opsx:verify`):
   - Полнота: все задачи выполнены, все требования реализованы
   - Корректность: соответствие spec intent
   - Связность: дизайн отражён в коде

7. **Archive** (`/opsx:archive`):
   - Delta specs merge в main specs (Source of Truth)
   - Change folder перемещается в `archive/`
   - Spec эволюционирует органически

#### Ключевые характеристики

- **Мастер-спецификация**: `openspec/specs/` — **Source of Truth**. Эволюционирует через archive. Delta specs merge в main specs при архивации.
- **Версионирование**: Git + `archive/` с date-prefix. Каждый change — отдельная папка с полным контекстом.
- **Обновляемость**: **Delta specs** — ключевая концепция. Описывают только изменения (ADDED/MODIFIED/REMOVED), а не полные спецификации. Механизм merge при archive.
- **Связи с кодом**: Артефакты — поведенческие контракты, код реализуется через `/opsx:apply`
- **Аудит**: Archive хранит полный контекст (proposal + design + tasks + specs) для каждого изменения
- **Состояние**: `changes/` (в процессе) + `archive/` (завершено). `config.yaml` хранит профиль (core/expanded)
- **Schemas**: Могут определять кастомные workflow (spec-driven, research-first и т.д.)

---

## 3. Сравнительные таблицы

### 3.1 Жизненный цикл документации

| Критерий | AI-DLC | Spec Kit | OpenSpec |
|----------|--------|----------|----------|
| **Подход** | Phase-based (3 фазы) | Spec-Driven (5 команд) | Delta-driven (fluid actions) |
| **Мастер-спецификация** | ❌ Отсутствует | ✅ Constitution (постоянная) | ✅ Specs (Source of Truth) |
| **Обновление мастер-спецификации** | ❌ Нет механизма | ✅ Constitution + фичи-ветки | ✅ Delta specs + archive merge |
| **Версионирование** | Git (внешнее) | Git branching + feature нумерация | Git + archive/ |
| **Delta-изменения** | ❌ Нет | ❌ Нет (полные перезаписи) | ✅ ADDED/MODIFIED/REMOVED |
| **Механизм merge** | ❌ Нет | ❌ Нет (Git merge) | ✅ Встроенный merge при archive |
| **Аудит-трейл** | ✅ `audit.md` (append-only) | ✅ Git history | ✅ Archive folder |
| **State tracking** | ✅ `aidlc-state.md` | ❌ Нет (Git branching) | ✅ `changes/` + `archive/` |
| **Можно ли вернуться назад** | ❌ Фазы последовательные | ✅ Ветки можно менять | ✅ Fluid, без gate |

### 3.2 Работа с требованиями

| Критерий | AI-DLC | Spec Kit | OpenSpec |
|----------|--------|----------|----------|
| **Бизнес-требования** | ✅ Business overview (brownfield) | ✅ User Stories + personas | ✅ Proposal (intent/scope) |
| **Системные требования** | ✅ Functional + NFR requirements | ✅ Functional Requirements (FR-001...) | ✅ Requirements с RFC 2119 |
| **Несистемные требования** | ✅ NFR (performance, security) | ✅ Non-functional через Constitution | ✅ Constraints в specs |
| **Приоритизация** | ❌ Нет явной | ✅ P1/P2/P3 user stories | ❌ Нет явной (scope в proposal) |
| **Acceptance criteria** | ✅ Acceptance scenarios | ✅ Given/When/Then | ✅ Scenarios (Given/When/Then) |
| **Измеримые критерии** | ⚠️ Частично | ✅ Measurable Outcomes | ⚠️ Через scenarios |
| **Управление изменениями** | ❌ Полная перегенерация | ✅ Новая фича (ветка) | ✅ Delta specs |
| **Неоднозначности** | ⚠️ Через вопросы | ✅ `[NEEDS CLARIFICATION]` | ✅ Progressive rigor |
| **Edge Cases** | ⚠️ В requirements | ✅ Dedicated section | ✅ В scenarios |

### 3.3 Разработка архитектуры

| Критерий | AI-DLC | Spec Kit | OpenSpec |
|----------|--------|----------|----------|
| **Архитектурный документ** | ✅ `architecture.md` | ✅ `plan.md` + `data-model.md` | ✅ `design.md` |
| **DDD/Units** | ✅ Units of Work + dependency | ❌ Нет DDD | ❌ Нет DDD |
| **Компоненты** | ✅ `components.md` | ✅ Project Structure | ❌ Нет |
| **Сервисы** | ✅ `services.md` | ❌ Нет | ❌ Нет |
| **API контракты** | ✅ `api-documentation.md` | ✅ `contracts/` (JSON+MD) | ❌ Нет (через specs) |
| **Технологический стек** | ✅ `technology-stack.md` | ✅ Technical Context | ⚠️ В design.md |
| **Инфраструктура** | ✅ `infrastructure-design.md` | ❌ Нет | ⚠️ В design.md |
| **Data Model** | ✅ `domain-entities.md` | ✅ `data-model.md` | ✅ В specs |
| **Decision log** | ❌ Нет | ⚠️ Complexity Tracking | ✅ Architecture Decisions |
| **Конституция/принципы** | ❌ Нет | ✅ 9 статей | ❌ Нет (schemas) |

### 3.4 Разработка спецификаций интеграций

| Критий | AI-DLC | Spec Kit | OpenSpec |
|--------|--------|----------|----------|
| **API контракты** | ✅ REST + internal APIs | ✅ JSON + Markdown | ❌ Нет |
| **Service contracts** | ✅ `services.md` | ⚠️ Через contracts/ | ❌ Нет |
| **Integration points** | ✅ `component-dependency.md` | ✅ `data-model.md` | ⚠️ В delta specs |
| **Data flow** | ✅ Component dependency graph | ✅ Data model + contracts | ⚠️ В design.md |
| **Technology constraints** | ✅ Technology stack doc | ✅ Technical Context | ⚠️ В proposal |
| **Testing contracts** | ✅ Contract test instructions | ✅ Contract tests mandatory | ❌ Нет |

### 3.5 Обновляемая мастер-спецификация

| Критерий | AI-DLC | Spec Kit | OpenSpec |
|----------|--------|----------|----------|
| **Наличие** | ❌ Нет | ✅ Constitution.md | ✅ Specs/ (Source of Truth) |
| **Формат** | N/A | Markdown, 9 articles | Markdown, RFC 2119 requirements |
| **Обновление** | ❌ Нет механизма | ✅ Constitution amendments | ✅ Delta specs merge |
| **Версионирование** | ❌ Нет | ✅ Git branching | ✅ Archive history |
| **Traceability** | ✅ Audit trail | ✅ Spec → Plan → Tasks | ✅ Proposal → Specs → Design → Tasks |
| **Drift detection** | ❌ Нет | ❌ Нет | ⚠️ Verify (post-implementation) |
| **Single Source of Truth** | ❌ Документы разрознены | ✅ Constitution | ✅ Specs/ directory |

### 3.6 Поддержка AI-агентов

| Критерий | AI-DLC | Spec Kit | OpenSpec |
|----------|--------|----------|----------|
| **Claude Code** | ✅ CLAUDE.md | ✅ Slash commands | ✅ Slash commands |
| **Cursor** | ✅ .cursor/rules | ✅ Slash commands | ✅ Slash commands |
| **GitHub Copilot** | ✅ copilot-instructions.md | ✅ Slash commands | ✅ Slash commands |
| **Cline** | ✅ .clinerules | ✅ Slash commands | ✅ Slash commands |
| **Amazon Q** | ✅ .amazonq/rules | ❌ Нет | ❌ Нет |
| **Kiro** | ✅ .kiro/steering | ❌ Нет | ❌ Нет |
| **OpenAI Codex** | ✅ AGENTS.md | ✅ Skills mode | ✅ Slash commands |
| **Gemini CLI** | ⚠️ AGENTS.md | ✅ Slash commands | ✅ Slash commands |
| **Другие** | ✅ Любые с rules | ✅ 30+ integrations | ✅ 25+ tools |
| **Установка** | Копирование файлов | Python CLI (uv/pipx) | Node CLI (npm) |
| **Зависимости** | Нет | Python 3.11+, Git | Node.js 20.19+ |

### 3.7 Расширяемость и кастомизация

| Критерий | AI-DLC | Spec Kit | OpenSpec |
|----------|--------|----------|----------|
| **Расширения** | ✅ Extensions (opt-in rules) | ✅ 80+ community extensions | ✅ Custom schemas |
| **Пресеты** | ❌ Нет | ✅ Community presets | ⚠️ Config YAML |
| **Кастомные workflow** | ⚠️ Through rule files | ✅ Workflow engine (YAML) | ✅ Schema definitions |
| **Пользовательские правила** | ✅ Добавление extensions | ✅ Project-local overrides | ✅ Config customization |
| **Интеграции** | ❌ Нет встроенных | ✅ Jira, Confluence, Azure | ⚠️ Community schemas |
| **Команды** | ⚠️ Через rules | ✅ 10+ slash commands | ✅ 10+ slash commands |

### 3.8 Brownfield vs Greenfield

| Критерий | AI-DLC | Spec Kit | OpenSpec |
|----------|--------|----------|----------|
| **Greenfield** | ✅ Inception Phase | ✅ 0-to-1 Development | ✅ Через proposal |
| **Brownfield** | ✅ Reverse Engineering | ✅ Brownfield Bootstrap | ✅ Brownfield-first |
| **Reverse engineering** | ✅ Полный (8 документов) | ⚠️ Через расширение | ❌ Нет |
| **Дельта-подход** | ❌ Нет | ❌ Нет | ✅ ADDED/MODIFIED/REMOVED |
| **Изоляция изменений** | ❌ Нет | ✅ Feature branches | ✅ Change folders |

---

## 4. Глубокий анализ по ключевым аспектам

### 4.1 Жизненный цикл документации

**AI-DLC** — наиболее структурированный подход с жёсткими фазами. Документация генерируется ИИ в момент запуска workflow и живёт в `aidlc-docs/`. Проблема: нет механизма обновления существующих документов — при каждом запуске они перезаписываются. Это делает AI-DLC подходящим для initial project setup, но слабым для ongoing development.

**Spec Kit** — подход с постоянным артефактом `constitution.md` (конституция проекта), который не меняется при каждом запуске. Функциональные спецификации живут в feature-ветках. Это обеспечивает версионирование, но нет механизма обновления одной спецификации — нужно создавать новую фичу. Workflow engine позволяет создавать сложные многоступенчатые процессы.

**OpenSpec** — самый гибкий подход к lifecycle. **Source of Truth** в `openspec/specs/` эволюционирует через **delta specs**. При archive дельта-спецификации merge в main specs, создавая живую, обновляемую мастер-спецификацию. Change folders изолируют параллельные работы. Archive обеспечивает полный аудит-трейл.

### 4.2 Разработка спецификаций интеграций

**AI-DLC** имеет лучший набор артефактов для интеграций: `api-documentation.md`, `component-dependency.md`, `services.md`, `contract-test-instructions.md`. Структурированный подход с DDD units makes it powerful for complex systems.

**Spec Kit** — `contracts/` директория с JSON API spec и Markdown контрактами. Обязательные contract tests перед имплементацией (Article IX). Data model документ для структуры данных.

**OpenSpec** — контракты описаны как part of specs (RFC 2119 requirements + scenarios). Нет специализированных артефактов для API контрактов, но это компенсируется простотой и гибкостью.

### 4.3 Разработка архитектуры

**AI-DLC** — наиболее глубокий архитектурный анализ: `application-design.md`, `components.md`, `component-methods.md`, `services.md`, `infrastructure-design.md`, `deployment-architecture.md`. DDD-based decomposition через Units of Work.

**Spec Kit** — `plan.md` с Technical Context, Project Structure, Constitution Check. `data-model.md` для модели данных. `research.md` для архитектурных исследований. Complexity Tracking для обоснования архитектурных решений.

**OpenSpec** — `design.md` с technical approach и architecture decisions. Architecture Decisions captured как ADR-подобная структура. Data flow diagrams. Лёгче, но менее структурировано.

### 4.4 Работа с бизнес-требованиями

**AI-DLC** — `business-overview.md` для brownfield (контекст бизнеса, транзакции, словарь). `requirements.md` для functional/non-functional. Question-driven approach.

**Spec Kit** — User Stories с приоритетами, INVEST-критерии, personas. `spec.md` с обязательными User Scenarios. Success Criteria — измеримые. Constitution задаёт бизнес-принципы.

**OpenSpec** — `proposal.md` с intent, scope, approach. Requirements в delta specs с RFC 2119. Scenarios как acceptance criteria. Progressive rigor — lite/full spec.

### 4.5 Системные и несистемные требования

**AI-DLC** — лучшая проработка: `nfr-requirements.md` (scalability, performance, availability, security) и `nfr-design-patterns.md` (resilience, scalability, performance, security patterns). NFR Requirements и NFR Design — отдельные фазы.

**Spec Kit** — NFR через Constitution (9 статей) + Technical Context в plan.md. Performance Goals, Constraints, Scale/Scope — обязательные поля.

**OpenSpec** — НСР через RFC 2119 keywords в specs (SHALL/MUST for hard constraints). Не явная, но flexible.

### 4.6 Обновляемая мастер-спецификация

Это критический аспект сравнения.

| | AI-DLC | Spec Kit | OpenSpec |
|--|--------|----------|----------|
| Мастер-спецификация | ❌ Нет | ✅ Constitution.md | ✅ Specs/ (evolving) |
| Обновление | ❌ Нет | ✅ Constitution amendments | ✅ Delta merge |
| Версионирование | ❌ Git only | ✅ Feature branches | ✅ Archive history |
| Single Source of Truth | ❌ Документы разрознены | ✅ Constitution | ✅ Specs/ directory |
| Drift detection | ❌ Нет | ❌ Нет | ✅ Verify post-implementation |

**OpenSpec** — единственный фреймворк с настоящим **живым** Source of Truth. Дельта-спецификации merge в main specs при archive, создавая continuously evolving specification. Это критически важно для brownfield проектов.

**Spec Kit** — Constitution.md является единственной постоянной мастер-спецификацией. Функциональные спецификации живут в feature-ветках, но нет механизма обновления одной спецификации.

**AI-DLC** — нет концепции мастер-спецификации. Все документы — разовая генерация при запуске workflow.

---

## 5. Рекомендации

### Выбор фреймворка по сценарию

| Сценарий | Рекомендация | Обоснование |
|----------|-------------|-------------|
| **Новый проект (greenfield)** | **Spec Kit** | Полная структура, constitution, TDD-first, 30+ integrations |
| **Brownfield проект** | **OpenSpec** | Delta specs — идеально для incremental изменений |
| **Enterprise (AWS stack)** | **AI-DLC** | Нативная поддержка Amazon Q, Kiro, AWS patterns |
| **Нужна мастер-спецификация** | **OpenSpec** | Единственный с evolving Source of Truth |
| **Нужна конституция/принципы** | **Spec Kit** | 9 articles enforced through templates |
| **Сложная архитектура (DDD)** | **AI-DLC** | Units of Work, components, services, dependencies |
| **Быстрый старт** | **OpenSpec** | `openspec init` + `/opsx:propose`, минимум зависимостей |
| **Много интеграций (Jira, Confluence)** | **Spec Kit** | 80+ community extensions |
| **Нужен audit trail** | **AI-DLC** | `audit.md` append-only log |
| **Минимальные зависимости** | **OpenSpec** | Node.js CLI, markdown-файлы |

### Комбинированный подход

Для максимального покрытия рекомендуется:

1. **Spec Kit** для greenfield инициации и constitution-driven principles
2. **OpenSpec** для ongoing brownfield development с delta specs
3. **AI-DLC** для enterprise-уровня архитектурного анализа (brownfield reverse engineering)

---

## 6. Итоговая сводная таблица

| Критерий | AI-DLC | Spec Kit | OpenSpec |
|----------|:------:|:--------:|:--------:|
| **Зрелость** | Высокая | Высокая | Средняя |
| **Структура** | Очень высокая | Высокая | Лёгкая |
| **Brownfield** | Хороший | Хороший | Лучший |
| **Greenfield** | Хороший | Лучший | Хороший |
| **Мастер-спецификация** | ❌ | ✅ Constitution | ✅ Specs |
| **Delta-изменения** | ❌ | ❌ | ✅ |
| **Merge specs** | ❌ | ❌ | ✅ |
| **Audit trail** | ✅ | ⚠️ Git | ✅ Archive |
| **AI-агенты** | 8+ | 30+ | 25+ |
| **Расширения** | Extensions | 80+ community | Custom schemas |
| **Зависимости** | Нет | Python | Node.js |
| **DDM/Units** | ✅ | ❌ | ❌ |
| **Конституция** | ❌ | ✅ | ❌ |
| **Workflow engine** | ❌ | ✅ YAML | ⚠️ Schemas |
| **Установка** | Копирование | CLI install | CLI install |

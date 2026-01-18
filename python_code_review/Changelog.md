# Changelog

Все заметные изменения в промптах для Python Code Review.

Формат основан на [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [2.0.0] - 2025-01-17

### Разделение на модули
- **BREAKING**: Промпт разделён на 3 файла:
  - `code_review_prompt.md` — основной промпт
  - `docker_review_prompt.md` — Docker-специфичные проверки
  - `testing_review_prompt.md` — тестирование и примеры тестов

### Добавлено
- `<check_order>` — приоритет проверок (Security → Correctness → Error handling → Architecture → Style)
- `<code_complexity_detection>` — автоматическое определение простого/сложного кода
- `<common_mistakes_examples>` — 7 типичных ошибок с примерами [FAIL]/[OK]
- `<output_example>` — полный пример ожидаемого отчёта
- `<modularization>` — формат вывода с Migration Plan для LOC > 500
- Конкретные критерии оценки в `<grade>` (0 critical, ≤2 important = Отлично)
- Оценка времени исправления в секции `<fixes>`

### Изменено
- Секция `<modules>` уточнена: применяется только при LOC > 500 → src/
- Формат вывода упрощён с 12 секций до 5 основных
- Docker проверки вынесены в отдельный файл
- Примеры тестов вынесены в отдельный файл

### Удалено
- `<context_analysis>` с 7 вопросами — избыточно, LLM редко задаёт уточняющие вопросы
- `<genius_approach>` — субъективно и размыто
- `<line_by_line>` построчные комментарии — нереалистично для больших файлов
- `<todo>TODO: crbug.com/ID` — слишком специфично (Chromium)
- Дублирование правил imports (было в 3 местах)
- Детальный `<dockerfile_review>` из основного промпта (перенесён в docker_review_prompt.md)

---

## [1.0.0] - 2025-01-17

### Начальная версия
- Монолитный промпт (~450 строк XML)
- Поддержка Google Style Guide
- Поддержка Hitchhiker's Guide to Python
- Docker Environment проверки (встроенные)
- Контекстный анализ с вопросами
- Формат вывода с 12 секциями
- Функциональный подход (без OOP)

---

## Docker Review Prompt

### [1.1.0] - 2025-01-17

#### Добавлено
- CVE security scanning в чеклисте
- `<example_output>` для Dockerfile review
- Детальные примеры graceful shutdown с SIGINT
- Пример Docker secrets с fallback на ENV

---

## Testing Review Prompt

### [1.1.0] - 2025-01-17

#### Добавлено
- `<edge_cases_to_test>` — маппинг функций к конкретным тестам
- Примеры тестов для collection operations
- Примеры тестов для file operations с tmp_path
- 6-й антипаттерн: Global state pollution
- `<test_fixtures_recommendations>` — pytest fixtures
- Примеры custom fixtures

---

## Documentation Prompt

### [1.0.0] - 2025-01-17

#### Добавлено
- Шаблоны для README.md, CHANGELOG.md, CONTRIBUTING.md
- Шаблоны для docs/API.md, docs/TESTING.md, docs/ARCHITECTURE.md
- Формат docstrings (Google Style)
- Вспомогательные файлы: .gitignore, pyproject.toml, LICENSE
- Пошаговый процесс генерации документации

---

## Architecture as Code Prompt

### [1.0.0] - 2025-01-17

#### Добавлено
- 8 типов диаграмм: System Context, Container, Module Dependencies, Data Flow, Sequence, Deployment, ER, State Machine
- Полный справочник Graphviz DOT синтаксиса
- 4 цветовые схемы: default, C4 Model, status, layers
- 8 готовых шаблонов диаграмм с примерами
- Анализ кода: извлечение зависимостей, метрики coupling/cohesion
- Подсветка проблем: циклические зависимости, god modules, orphans
- Процесс генерации диаграмм из кода
- Команды рендеринга (PNG, SVG, PDF)
- Интеграция в документацию

---

## CI/CD Prompt

### [1.0.0] - 2025-01-17

#### Добавлено
- GitHub Actions полный шаблон с 5 stages
- GitHub Actions минимальный шаблон
- GitHub Actions reusable workflow
- GitLab CI полный шаблон с templates
- GitLab CI минимальный шаблон
- GitLab CI child pipelines для монорепо
- Matrix testing (multiple Python versions + OS)
- Services: PostgreSQL, Redis
- Docker build с multi-stage
- Security scanning: bandit, pip-audit, CodeQL
- Deployment: staging, production с environments
- Best practices: security, performance, reliability
- Common patterns: caching, artifacts, notifications, scheduled runs
- Dockerfile оптимизированный для CI
- Список required secrets

---

## Security Review Prompt

### [1.0.0] - 2025-01-17

#### Добавлено
- 10 категорий проверок безопасности с приоритизацией
- CWE references для всех уязвимостей
- Примеры [CRITICAL]/[HIGH]/[MEDIUM]/[LOW] с кодом
- Инъекции: SQL, Command, Code, SSTI, XPath
- Authentication: password hashing, token generation, timing attacks
- Secrets: hardcoded credentials, logs, version control
- Cryptography: weak algorithms, key length, random generation
- Input validation: path traversal, open redirect, ReDoS
- File operations: upload, temp files, permissions
- Deserialization: pickle, YAML, XML bombs
- Dependencies: CVE checking, dependency confusion
- Logging: sensitive data, log injection
- Configuration: debug mode, default credentials, CORS
- Security tools: bandit, semgrep, pip-audit, detect-secrets
- Формат отчёта с severity levels

---

## Makefile Prompt

### [1.0.0] - 2025-01-17

#### Добавлено
- Полный шаблон Makefile для Python проектов
- Варианты таргетов: minimal, standard, full, library, cli_tool, web_service
- Специализированные таргеты: database, web_server, security, docker_compose
- Best practices для Makefile
- Примеры для разных типов проектов
- Автогенерируемый help с цветным выводом

---

## Планы на будущее

### Возможные улучшения
- [ ] Промпт для async/await кода
- [ ] Промпт для type checking (mypy интеграция)
- [ ] Промпт для database review (SQL, ORM, migrations)
- [ ] Промпт для API design review (REST, GraphQL)
- [ ] Промпт для pre-commit hooks конфигурации

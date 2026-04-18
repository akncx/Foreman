# Foreman

[English version](./README.md)

Foreman — это plugin-first пакет оркестрации для Factory Droid.

Он превращает основной чат в оркестратор репозитория: агент исследует проект, разбивает задачу на независимые потоки работы, предлагает план и запускает реальные worker-subagent’ы для выполнения.

Канонический репозиторий:
- `https://github.com/akncx/Foreman`

## Что даёт этот плагин

- slash-entrypoint `/foreman`
- переиспользуемый orchestration skill `foreman`
- droid `foreman` для координации
- droid `worker` для делегированного выполнения

## Модель работы

- основной чат = оркестратор
- `worker` subagent’ы = исполнители
- один независимый workstream обычно соответствует одной ветке и одному worktree
- исследование репозитория происходит локально через инструменты Droid, а не через web fetch
- runtime state при необходимости хранится в целевом репозитории в `.foreman/`

## Пример

```text
/foreman Refactor A, B, C
```

Ожидаемое поведение:

1. исследовать текущий репозиторий
2. разбить запрос на workstream’ы, если это безопасно
3. предложить краткий план
4. после подтверждения определить стратегию branch/worktree
5. запустить `worker` subagent’ов через `Task`
6. собрать результаты и прогнать валидацию

## Foreman vs Droid Missions

Foreman не пытается заменить Missions. Это более лёгкий orchestration layer для задач среднего размера внутри репозитория.

### Где Foreman лучше

- меньше overkill для средних задач
- ниже token overhead для chat-driven orchestration
- больше прямого контроля над worker’ами, branch и worktree strategy
- легче кастомизировать через skill и droid prompts
- быстрее как entrypoint для repo-local multi-step работы

### Где Missions лучше

- сильнее встроенная структура для более крупных инициатив
- более нативный managed workflow внутри Droid
- лучше подходят для тяжёлого multi-phase planning и execution

### Практическое правило выбора

- используй **Foreman** для задач среднего размера, когда нужен явный orchestration workflow с меньшим overhead
- используй **Missions** для более больших, длинных и структурированных инициатив, где дополнительный framework оправдан

## Структура репозитория

- `.factory-plugin/marketplace.json` — manifest single-plugin marketplace
- `.factory-plugin/plugin.json` — manifest плагина
- `skills/foreman/SKILL.md` — orchestration logic
- `droids/foreman.md` — coordinating droid
- `droids/worker.md` — execution droid

## Локальная разработка

Установка из локальной директории:

```bash
droid plugin marketplace add .
droid plugin install foreman@Foreman
```

Затем вызов:

```text
/foreman <ваш запрос>
```

## Установка из GitHub marketplace source

Этот репозиторий опубликован как single-plugin marketplace.

Добавьте репозиторий как marketplace source:

```bash
droid plugin marketplace add https://github.com/akncx/Foreman
```

Установите плагин:

```bash
droid plugin install foreman@Foreman
```

Позже обновляйте так:

```bash
droid plugin update foreman@Foreman
```

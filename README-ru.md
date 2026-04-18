# Foreman

[English version](./README.md)

Foreman — это плагин для Factory Droid.

Он помогает основному чату выступать координатором работы в репозитории: разбивать задачу на части, запускать worker'ов и вести следующие шаги.

Канонический репозиторий:
- `https://github.com/akncx/Foreman`

## Что даёт этот плагин

- команда `/foreman`
- переиспользуемый skill `foreman`
- droid `foreman` для координации
- droid `worker` для делегированного выполнения

## Модель работы

- основной чат = оркестратор
- `worker` subagent’ы = исполнители
- один независимый workstream обычно соответствует одной ветке и одному worktree
- плагин может разбивать работу на отдельные задачи, когда это полезно
- при необходимости он может хранить task context в `.foreman/` внутри целевого репозитория

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

Foreman не пытается заменить Missions. Это более лёгкий вариант для задач среднего размера внутри репозитория.

### Где Foreman лучше

- меньше overkill для средних задач
- меньше расход токенов и меньше overhead
- больше прямого контроля над worker’ами, branch и worktree strategy
- легче кастомизировать
- быстрее запускать для обычных задач в репозитории

### Где Missions лучше

- сильнее встроенная структура для более крупных инициатив
- лучше подходят для тяжёлого multi-phase planning и execution

### Практическое правило выбора

- используй **Foreman** для задач среднего размера, когда нужен явный orchestration workflow с меньшим overhead
- используй **Missions** для более больших, длинных и структурированных инициатив, где дополнительный framework оправдан

## Структура репозитория

- `.factory-plugin/marketplace.json` — manifest single-plugin marketplace
- `.factory-plugin/plugin.json` — manifest плагина
- `skills/foreman/SKILL.md` — основной skill
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

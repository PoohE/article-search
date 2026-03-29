# Skill: search-all
Запускает ежемесячный поиск статей по всем трём темам последовательно.
Вызов: `/search-all`

Используй агентов: `researcher-global-landcover`, `researcher-historical-lulc`, `researcher-mountain-treeline`.

## Перед запуском

Сообщи пользователю:
```
Запускаю поиск по 3 темам:
  1. Глобальные покрытия (спутниковая съёмка)
  2. Историческая картография и LULC
  3. Верхняя граница леса и горные ландшафты

Результаты → D:\Dropbox\Project\PHD\Articles\article-search\
```

## Workflow

```
ШАГ 1  researcher-global-landcover
         Поиск + дедупликация + сохранение topic1
         ↓
ШАГ 2  researcher-historical-lulc
         Поиск + дедупликация + сохранение topic2
         ↓
ШАГ 3  researcher-mountain-treeline
         Поиск + дедупликация + сохранение topic3
```

Запускай агентов **последовательно** (не параллельно) — чтобы видеть прогресс по каждой теме.

## После завершения

Выведи итоговую сводку:
```
## Результаты поиска [дата]

| Тема | Новых статей | Файл |
|------|-------------|------|
| Глобальные покрытия | N | topic1_global_landcover/ГГГГ-MM_... |
| Историческая картография | N | topic2_historical_lulc/ГГГГ-MM_... |
| Граница леса / горы | N | topic3_mountain_treeline/ГГГГ-MM_... |

Все файлы сохранены в D:\Dropbox\Project\PHD\Articles\article-search\
```

## Запуск одной темы

Если нужна только одна тема — запускай напрямую:
- `/search-global-landcover` → только агент researcher-global-landcover
- `/search-historical-lulc` → только агент researcher-historical-lulc
- `/search-mountain-treeline` → только агент researcher-mountain-treeline

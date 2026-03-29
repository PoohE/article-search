# Skill: search-all-remote
Удалённая версия поиска статей по всем трём темам.
Используется только в remote trigger (GitHub Actions / CCR).
Сохраняет результаты в репозиторий, делает git commit + push.

## Workflow

```
ШАГ 1  researcher-global-landcover-remote
         Поиск + дедупликация → results/topic1_global_landcover/ → git commit
         ↓
ШАГ 2  researcher-historical-lulc-remote
         Поиск + дедупликация → results/topic2_historical_lulc/ → git commit
         ↓
ШАГ 3  researcher-mountain-treeline-remote
         Поиск + дедупликация → results/topic3_mountain_treeline/ → git commit
```

Запускай агентов **последовательно**.

## После завершения

Выведи итоговую сводку:
```
## Автопоиск завершён [дата]

| Тема | Новых статей | Файл |
|------|-------------|------|
| Глобальные покрытия | N | results/topic1_global_landcover/ГГГГ-MM_... |
| Историческая картография | N | results/topic2_historical_lulc/ГГГГ-MM_... |
| Граница леса / горы | N | results/topic3_mountain_treeline/ГГГГ-MM_... |

Результаты сохранены в репозиторий: https://github.com/PoohE/article-search
```

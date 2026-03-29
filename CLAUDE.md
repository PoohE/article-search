# Проект: Ежемесячный поиск статей

## Тип задач
Автоматический ежемесячный поиск новых научных статей по трём независимым темам.
Каждая тема имеет свой архив — повторы не возникают между темами.
Каждый запуск возвращает только новые результаты относительно предыдущих.

## Область
Географические и биологические науки: география, науки о Земле, биология,
фитоценология, ландшафтоведение, историческая география, картография,
дистанционное зондирование, ГИС, ландшафтное моделирование, биоразнообразие.

## Запуск вручную
- Все три темы сразу: `/search-all`
- Только тема 1: запусти агент `researcher-global-landcover`
- Только тема 2: запусти агент `researcher-historical-lulc`
- Только тема 3: запусти агент `researcher-mountain-treeline`

## Расписание
Ежемесячно (1-й понедельник месяца). Темы фиксированы в файлах `topics/`.

---

## Три темы поиска

| # | Тема | Агент | Архив |
|---|------|-------|-------|
| 1 | Глобальные покрытия (спутниковая съёмка) | researcher-global-landcover | archive/all_found_topic1.md |
| 2 | Историческая картография, LULC, динамика ландшафтов | researcher-historical-lulc | archive/all_found_topic2.md |
| 3 | Верхняя граница леса, горные ландшафты | researcher-mountain-treeline | archive/all_found_topic3.md |

---

## Workflow

```
/search-all
    │
    ├── ШАГ 1  researcher-global-landcover
    │            Читает topics/topic1_global_landcover.md
    │            Ищет EN + RU источники
    │            Дедуплицирует по archive/all_found_topic1.md
    │            Сохраняет → Dropbox/topic1_global_landcover/
    │
    ├── ШАГ 2  researcher-historical-lulc
    │            Читает topics/topic2_historical_lulc.md
    │            Ищет EN + RU источники
    │            Дедуплицирует по archive/all_found_topic2.md
    │            Сохраняет → Dropbox/topic2_historical_lulc/
    │
    └── ШАГ 3  researcher-mountain-treeline
                 Читает topics/topic3_mountain_treeline.md
                 Ищет EN + RU источники
                 Дедуплицирует по archive/all_found_topic3.md
                 Сохраняет → Dropbox/topic3_mountain_treeline/
```

---

## Структура папок

```
article-search/                          ← рабочая папка (D:\Work\Claude\article-search\)
├── topics/
│   ├── topic1_global_landcover.md       # тема 1 (редактировать вручную при необходимости)
│   ├── topic2_historical_lulc.md        # тема 2
│   └── topic3_mountain_treeline.md      # тема 3
├── archive/
│   ├── all_found_topic1.md              # DOI найденных статей по теме 1
│   ├── all_found_topic2.md              # DOI найденных статей по теме 2
│   └── all_found_topic3.md              # DOI найденных статей по теме 3
└── .claude/
    ├── agents/
    │   ├── researcher-global-landcover.md
    │   ├── researcher-historical-lulc.md
    │   ├── researcher-mountain-treeline.md
    │   └── deduplicator.md              # утилита (не используется напрямую)
    └── skills/
        ├── search-all.md                # /search-all — запуск всех трёх
        └── search-articles.md           # устаревший (одна тема)

D:\Dropbox\Project\PHD\Articles\article-search\   ← результаты
├── topic1_global_landcover\
│   └── 2026-04_global-landcover.md
├── topic2_historical_lulc\
│   └── 2026-04_historical-lulc.md
└── topic3_mountain_treeline\
    └── 2026-04_mountain-treeline.md
```

---

## Базы данных

**Англоязычные:**
- Google Scholar
- Semantic Scholar
- EarthArXiv (препринты геонаук)
- arXiv (разделы cs.CV, eess.IV — для тем с ДЗЗ)
- PubMed (для биологических тем)
- JSTOR (для исторических тем)

**Русскоязычные:**
- КиберЛенинка (cyberleninka.ru)
- eLIBRARY.ru (РИНЦ)
- Google Scholar (русские запросы)

---

## Критерии качества статей

**Англоязычные:**
- Есть DOI
- Есть аффилиация авторов
- Не входит в список хищнических журналов (beallslist.net)

**Русскоязычные:**
- Есть в eLIBRARY.ru или КиберЛенинке
- Есть название журнала и авторы

---

## Глубина поиска

- **Первый запуск** (архив пуст) → последние 12 месяцев
- **Последующие запуски** → последний 1 месяц

---

## Напоминания для Claude

- Уточняющие вопросы задавать **по одному**, не списком
- Использовать модель **claude-opus-4-6**
- Никогда не добавлять в результаты статьи из архива
- Фиксировать дату поиска и число найденных / новых статей
- Не перезаписывать старые файлы результатов — создавать новые по месяцам
- Для русскоязычных статей без DOI — давать ссылку на страницу в eLIBRARY / КиберЛенинке

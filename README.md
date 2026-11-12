# dota-draft — Dota 2 draft analyst skill for Claude

Кидаешь скрин пик-фазы в чат Claude — получаешь, кто на какой позиции, как стоят лайны,
тайминги, план на игру и подсказки на пик. Данные берутся **по текущему патчу**: скилл каждый
раз сам ищет актуальную версию патча и мету (Dota2ProTracker, Dotabuff, Liquipedia,
сайты на базе OpenDota), а не опирается на устаревшую память модели.

> English summary below.

## Возможности

- **Быстрый режим** — для живой пик-фазы. Срабатывает, если драфт не закончен или ты пишешь
  «быстро» / «кого пикнуть». 1–2 поиска, ответ в 5 строк: три варианта пика на твой слот
  и главная угроза у врага.
- **Полный разбор** — когда драфт закрыт. Патч, позиции 1–5 и роль каждого героя в этом драфте,
  лайны, тайминги и win conditions обеих команд, угрозы для твоей команды, вердикт и источники.
- Распознаёт героев со скриншота; если портрет нечитаемый, помечает героя знаком «(?)», а не выдумывает.
- Не придумывает винрейты: если цифру не нашёл, описывает матчап словами.
- Отвечает на языке пользователя.

## Установка

### claude.ai (браузер, десктоп-приложение)

Нужны выполнение кода и веб-поиск (оба включаются в настройках).

1. Скачай `dota-draft.zip` со страницы [Releases](../../releases) — не распаковывай.
2. Открой **Customize → Skills** → **«+» → Create skill → Upload a skill** и выбери zip.
3. Проверь, что переключатель у dota-draft включён.

Собрать zip самому: `zip -r dota-draft.zip dota-draft` (в архиве должна быть папка `dota-draft/`
с `SKILL.md` внутри — имя папки должно совпадать с `name` в скилле).

### Claude Code

```bash
git clone https://github.com/YOUR_GITHUB_USERNAME/dota-draft-skill.git
cp -r dota-draft-skill/dota-draft ~/.claude/skills/
```

## Как пользоваться

| Когда | Что делать | Что получишь |
|---|---|---|
| До игры | «Мой пул: X, Y, Z. Кого пикать против меты текущего патча?» | Заготовки контрпиков |
| Пик-фаза | Скрин + «быстро». Кидай, как только видишь первые вражеские пики | 3 пика на твой слот + главная угроза |
| После драфта / загрузка | Финальный скрин + «разбор» | Полный план на игру |

Если скилл не подхватился сам — напиши «используй dota-draft».
Для быстрого режима можно выбрать более быструю модель.

## Ограничения

- Dota2ProTracker и Dotabuff блокируют прямое чтение страниц ботами, поэтому их цифры берутся
  из поисковых сниппетов, а подробности — с Liquipedia и OpenDota-сайтов. Полную таблицу меты
  скилл не видит.
- Полный разбор занимает примерно 30–60+ секунд (зависит от модели и нагрузки) — на один ход пика
  не успевает, для этого есть быстрый режим.
- Статистика — это тенденция, а не гарантия победы.

## English

A Claude skill that analyses Dota 2 drafts from a pick-screen screenshot using **current-patch** data
(it looks up the live patch and meta every time instead of trusting model memory).
*Fast mode* (incomplete draft or "fast"): 1–2 searches, top-3 picks for your slot plus the main threat.
*Full mode*: roles, lanes, timings, win conditions, threats, verdict, sources.
Install on claude.ai via **Customize → Skills → Upload a skill** with `dota-draft.zip` from Releases
(code execution and web search must be enabled), or copy `dota-draft/` into `~/.claude/skills/` for Claude Code.

## Disclaimer

Неофициальный фан-проект. Не связан с Valve, Dotabuff, Dota2ProTracker, Liquipedia или Anthropic.
Dota 2 — товарный знак Valve Corporation.

## Лицензия

[MIT](LICENSE)
# dota2-draft-analysis-skill

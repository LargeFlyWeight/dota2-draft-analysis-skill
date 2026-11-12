# Pro-match analysis mode (/dota-draft-pro)

Runs only when the user's message starts with `/dota-draft-pro`.

Goal: full pre-match / in-series analytics that people often use when looking at bets on
a match. Go beyond the heroes - factor in **who** is playing them. Teams, players, their
signature heroes, current form and head-to-head, combined with the draft read from SKILL.md.
Main use case is pro / tournament matches. Pub mode (random players) is at the end.

This mode needs more lookups (roughly 10-20 searches), so it is NOT for the live pick phase.
If the user adds "быстро", cap at ~5 searches and output only Форма, Игроки и герои, Вердикт.

## Step 1 - Identify the match

- Teams, tournament, stage, format (Bo1/Bo3/Bo5), game number and current series score,
  Radiant/Dire side. Take them from the screenshot overlay or the user's message.
- Rosters with positions 1-5: check Liquipedia for the current roster and any **stand-ins**
  for this event. A stand-in changes everything - always flag it.
- If you can't tell which match it is, say what you assumed in one line and continue.

## Step 2 - Team form (current patch first)

Search Liquipedia, bo3.gg, hawk.live, Dotabuff esports, STRATZ / datdota articles, news:
- Last ~10 series: results, opponents' level (tier-1 vs tier-2), tournament placings.
- Results on the **current patch** specifically - form from an older patch counts for less.
- Head-to-head between these teams in the last ~6 months (series and map score).
- Roster changes, stand-ins, recent coach changes, or notable news that affects form.
- Playstyle, if sources describe it: fast fighting/early aggression vs late-game, favourite
  strategies, what they tend to first-pick or ban.

## Step 3 - Players and their heroes

For each player (prioritise cores and the heroes actually picked in this draft):
- Signature heroes in the current patch: games and winrate in pro matches; pub spam
  (Dota2ProTracker player pages often show recent high-MMR pub heroes).
- Is the hero they got in THIS draft in their comfort pool, a new/rare pick, or a hero
  they have struggled on? This is often more important than the hero's global winrate.
- Individual form if sources mention it (MVP-level tournament, slump, recent role swap).
- Sources: Dota2ProTracker, Dotabuff esports player pages, Liquipedia player pages,
  datdota, recent tournament stat recaps. Use search snippets when pages block fetching.

## Step 4 - Combine with the draft

Run the full draft analysis from SKILL.md (roles, lanes, timings, win conditions), then
adjust it with what you learned: does the draft fit each team's style? Did a team pick into
its players' comfort or get banned out of it? Which player matchup on the lanes decides
the game?

## Output

Keep it scannable. Reply in the user's language.

**Матч:** teams, tournament/stage, format, series score, patch.
**Форма:** each team in one or two lines - recent record (with dates), notable wins/losses,
results on the current patch, stand-ins/roster news.
**Личные встречи:** head-to-head summary with dates, or "нет свежих данных".
**Игроки и герои:** per team, highlight who is on a signature hero, who is on an unusual
pick, and the biggest comfort gap. Don't list all ten players if there's nothing to say.
**Драфт:** short version of the full draft analysis (roles, lanes, timings, win conditions).
**Ключевые дуэли:** 2-3 player/lane matchups that decide the game.
**Вердикт:** who is favoured and why, with a confidence level (низкая / средняя / высокая).
**Коэффициенты** (only if the user gave bookmaker odds): convert them to implied
probability (1 / decimal odds, mention the bookmaker margin), and say in one line whether
your analysis leans further toward one side than the market does or roughly agrees with it.
Do not tell the user to bet, which side to bet on, or how much.
**Источники:** sites used and how fresh the data is.

**Disclaimer - ALWAYS the last line of every /dota-draft-pro answer, no exceptions,
including the "быстро" version.** Use exactly this text (translate it if replying in
another language):

> Это аналитика, а не совет. Если вы используете её для ставок на матч: скилл ничего не гарантирует и не рекомендует делать ставки. Ставки — только 18+, если они легальны в вашей стране, и только на деньги, которые не жалко потерять.

## Rules

- Never invent stats, results or rosters. Every number gets a date range or "текущий патч".
- Flag small samples (fewer than ~5 games) as unreliable.
- Present the verdict as a lean with reasons, never as a certainty. Upsets are common.
- Betting: give the full analysis, but never recommend placing a bet, a side to bet on,
  stake sizes, bankroll strategies or "express" combinations, and never call anything a
  "лок", "верняк" or "гарантия". The disclaimer above covers the rest - don't lecture beyond it.
- If the user sounds like they are chasing losses or betting money they can't afford, drop
  the analysis tone for a moment, say it kindly, and mention that help with gambling
  problems exists (no need to list hotlines unless asked).

## Pub games (ranked with random players)

If `/dota-draft-pro` is used on a pub screenshot with visible nicknames:
- Search for public Dotabuff / OpenDota / STRATZ profiles by nickname. Many profiles are
  hidden or nicknames are ambiguous - if so, say so and skip that player rather than guess.
- Use only in-game stats: most played heroes, winrate on the picked hero, recent form.
  Nothing about the person beyond their Dota stats.
- Keep it to the 1-3 most informative findings (e.g. "их керри - 300 игр на Анти-Маге,
  62%"). Pub lookups are slow, so do this after the draft, not during picks.

---
name: dota-draft
description: Dota 2 draft analyst working from CURRENT patch data. Use this skill whenever the user sends a screenshot of a Dota 2 pick screen, draft, scoreboard or hero lineup, lists Dota heroes for two teams, types /dota-draft, or asks who plays which role, who wins a lane, what a draft wants to do, counterpicks, or "кто что делает" in a Dota game - even if they don't say the word "draft". Always looks up the live patch, pro/tournament meta and high-MMR stats (Dota2ProTracker, Dotabuff, Liquipedia, OpenDota-based sites) instead of relying on memory.
---

# Dota Draft Analyst

## FAST MODE - check this first

Use fast mode when the draft is incomplete (empty slots, someone is still picking) OR the
user writes "быстро", "fast", "пик", "кого пикнуть" or similar. The user has only a few
seconds of pick time, so speed beats depth:

- At most 1-2 web searches total (e.g. "dota2protracker <key enemy hero> counters" and/or
  "dotabuff <key enemy hero> counters"). Skip the separate patch lookup; mention the patch
  only if a search result shows it.
- No long reasoning. Answer in at most 5 short lines:
  1. Top 3 picks for the user's open slot/role, each with a few words on why.
  2. One line: the single enemy hero/combo to respect most.
- Then stop. Offer the full breakdown (below) for after the draft is locked.

Otherwise (draft complete, or user asks for full analysis) use the full workflow below.

The user drops a draft (usually a screenshot of the pick screen) and wants a fast, practical
read: who plays what, how lanes go, what each team wants to do, and what to watch out for.
Everything must reflect the **current** patch. Old-patch knowledge is the main failure mode
of this skill, so treat your own memory of hero numbers, winrates and meta as stale by default.

Reply in the user's language (usually Russian, casual gamer slang is fine).

## Step 1 - Read the draft

- Identify all visible heroes for Radiant and Dire, plus bans if shown.
- Figure out which team is the user's (highlighted slot, "you" marker, bottom/left side, or
  what they said). If you can't tell, assume and say so in one short line - don't stop to ask.
- If a portrait is unclear, say which slot you're unsure about and give your best guess
  marked with "(?)". Never silently invent a hero.
- If the draft is incomplete (mid-pick), analyse what's there and suggest picks for the
  remaining slots.

## Step 2 - Pin down the current patch (always, every time)

Run a web search (`web_search` in claude.ai, `WebSearch` in Claude Code) for the latest Dota 2 patch (e.g. "Dota 2 latest patch", "Dota 2 patch notes").
Note the current version and date. Then, for every hero in the draft that you plan to say
something specific about, check whether it was changed in the latest patch/letter patches
(search "<hero> <patch version>" or "<patch version> nerfs buffs").
Anything you remember about ability values, facets, talents or items may be outdated - if
it matters for your verdict, verify it or don't state it.

## Step 3 - Pull current meta data

Dota2ProTracker and Dotabuff block direct page fetching (bot protection), so:

1. Search the web using the site names in the query, e.g.
   "dota2protracker <hero>", "dotabuff <hero> counters", "dotabuff <hero> win rate this week".
   Use what the snippets show (winrate, position, builds). You may try fetching (`web_fetch` / `WebFetch`) a
   returned URL once; if it's blocked, move on - don't retry.
2. Fallbacks that usually open: Liquipedia (tournament hero pick/ban stats for the current
   patch, recent big tournaments), dota2protips and other OpenDota-based meta pages,
   STRATZ articles, recent esports news on the patch meta.
3. Prefer data clearly labelled with the current patch or "this week/last 7 days".
   Ignore anything labelled with an older patch.

Budget: aim for roughly 5-10 searches total. The user is likely in the draft phase or about
to load in, so speed matters more than exhaustiveness. Focus lookups on the heroes and
matchups that actually decide the game, not all ten heroes equally.

Never make up numbers. If you didn't find a stat, describe the matchup qualitatively and
don't attach a percentage to it.

## Step 4 - Answer

Keep it short and scannable - the user will read this in 30-60 seconds. Structure:

**Patch:** version + one line on whether anything relevant changed for these heroes.

**Who plays what** - for each team, one line per hero: position (1-5), lane, and their job
in this specific draft (e.g. "pos 3, offlane - initiator, Blink + Ravage into BKB-less cores").
If a hero is flexed and the role is ambiguous, give the most likely one and the alternative.

**Lanes** - safe lane / mid / off lane: who's favoured and why, in one line each.

**Timings & win conditions** - when each team is strongest (early fight, 20-min push,
late game), what each team wants to do, and the key item timings (BKB, Blink, etc.).

**Threats for your team** - 2-4 bullet points: the enemy heroes/combos to respect and the
specific answer (item, positioning, target priority).

**Verdict** - one or two sentences: who the draft favours on paper and the single most
important thing the user's team must do to win.

**Sources** - one line naming where the meta data came from (e.g. "D2PT / Dotabuff snippets,
Liquipedia, patch 7.xx"), with links if you have them. If data was thin, say so honestly.

Remember that draft is only part of the outcome - frame stats as tendencies, not guarantees.

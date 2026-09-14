# Bot-Free Meeting Minutes — Agent Skill

Turn raw meeting notes or a Teams / Zoom / Google Meet transcript into executive-ready minutes — **without inviting an AI bot into your meeting.**

Works with any agent that reads `SKILL.md` (Claude Code, Claude.ai, Codex CLI, Gemini CLI, Cursor, and others).

## The problem this solves

Ask an AI to "summarize this meeting" and you get smooth sentences. Smooth sentences are the problem: to read well, the AI quietly turns things that were **not** decided into things that were.

| What was actually said | What a typical AI summary writes |
|---|---|
| "Let me look into that." | "Agreed to provide the feature." |
| "Almost done, just testing left." | "Payment module completed." |
| A wants to delay, B wants to push ahead (no agreement) | "Decided to adjust the schedule." |

Once the right-hand column is in a document, people act on it.

This skill works the opposite way: **decided and not-yet-decided go in physically separate boxes, and anything unclear goes in the lower box.** Gaps are never filled in — they become questions under "Needs Confirmation."

## Who this is for

- You write minutes for a manager, director, or executive.
- Your company blocks AI notetaker bots, or you'd rather not have one in the room.
- You already have notes or captions and just need them structured correctly.

## Install

```bash
npx skills add EthanusJS/bot-free-meeting-minutes
```

Or copy `skills/executive-meeting-minutes/` into your agent's skills folder (for Claude Code: `.claude/skills/`).

Then paste your notes and say something like: *"Make exec minutes from this for my VP — she cares about schedule slip and extra cost."*

## Output

`Bottom line` → `Decisions` → `Open / Disagreement` → `Risks` → `Action Items` (table) → `Needs Confirmation`

## How it compares

| | Writing by hand | "Summarize this" prompt | AI notetaker bots (Otter, Zoom AI Companion, etc.) | This skill |
|---|---|---|---|---|
| Bot joins the meeting | No | No | Yes | **No** |
| Separates decided vs. open | If you're careful | Rarely | Varies | **Enforced** |
| Keeps every number | Yes | Often drops some | Varies | **Rule: all numbers kept** |
| Missing owner/deadline | Easy to forget | Silently omitted | Varies | **Row kept as "TBD" + question** |
| Effort | High | Low | Lowest | Low |

If your company allows notetaker bots, tools like Fireflies are a good way to *capture* the transcript — you can still run that transcript through this skill.

## Tested

The underlying rules were developed over 13+ runs across Claude, ChatGPT, and Gemini, fixing specific failure modes: action-item tables disappearing, linked figures being dropped (e.g. 1,203 → 940 → 263 reduced to one number), and length limits causing approved items to be deleted.

## Limits (honest)

- **Text only.** Audio must be transcribed first.
- **Draft, not final.** Always verify numbers, dates, and names.
- **One situation.** This free skill covers executive reports only.
- Borderline phrasing like "we'll discuss it next time" is still classified inconsistently across models — though nothing is lost, since it also lands in Open / Disagreement and Action Items.
- Check your company's policy before pasting internal content into any AI tool.

## FAQ

**Can I use this in ChatGPT without skills support?**
Yes — paste the contents of `SKILL.md` into a new chat, then paste your notes.

**Why not just use an AI notetaker?**
If you can, use one to capture. This skill is about what gets written down as *decided*.

**Is there more?**
Client-meeting and weekly-check-in versions, plus Word templates and a usage guide, are in the full pack: https://pickenough.com/bot-free-minutes

## License

CC BY-NC 4.0 — free for personal and internal work use. No resale or redistribution as a paid product. See `LICENSE`.

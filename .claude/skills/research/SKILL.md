---
name: research
description: Build today's AI engineering research note. Research trusted and discovered sources, rank candidates against interests.md, and write a top-10 research note to inbox/ with Like / Not for me checkboxes. Use whenever the user runs /research, asks for today's AI news or morning research, or the 7am scheduled task fires.
---

# Daily AI engineering research

This skill usually runs unattended at 7am. Nobody is there to answer questions, so never stop to ask. When something is unclear or missing, make a sensible choice, keep going, and record what you did in the research note's "Run notes" section. The user reads those notes later and tunes the setup from them.

The goal is a short list the user will actually want to read, not a complete news feed. Ten well-chosen items beat thirty mediocre ones, and seven strong items beat ten padded with filler.

## Files in the vault

| File | Access | Purpose |
|---|---|---|
| `interests.md` | read only | The user's profile: core, learned, exploring, retired, not interested |
| `sources.md` | read only | Trusted sites to check first. If missing, use discovery only and note it |
| `seen.md` | read + append | Every URL ever shown, so nothing repeats |
| `inbox/` | write | Where today's research note goes |

Do not edit `interests.md` in this skill. The `/learn` skill owns all profile changes, because changes should be based on what the user liked, and likes only exist after /learn runs. Keeping one writer also prevents the two skills from overwriting each other.

## Steps

### 1. Check for an existing research note

Use the local date. If `inbox/YYYY-MM-DD Research.md` already exists for today, stop without changing anything. Scheduled tasks can run twice (for example a catch-up run after the computer wakes), and overwriting would erase checkboxes the user may already have ticked.

If `interests.md` is missing, write today's research note containing only a Run notes section explaining that, then stop.

### 2. Read context

Read `interests.md`, `sources.md`, and `seen.md`. Set the lookback window to everything published since the date of the most recent research note in `inbox/`, capped at 7 days. If there are no earlier research notes, use 5 days.

### 3. Gather candidates

Aim for roughly 25 to 40 candidates before filtering.

1. **Trusted sources first.** Check each site in `sources.md` for posts inside the lookback window.
2. **Discovery.** Search for recent material on each core and learned interest, and on each topic in the Exploring section. Use specific queries ("speculative decoding" rather than "AI inference").

For discovered sources, prefer primary and technical material: AI lab and company engineering blogs, arXiv and conference papers, official model announcements and technical reports, established practitioners' blogs, and reputable tech journalism. Skip SEO content farms, listicles, AI-generated roundups, vendor marketing without technical substance, and reposts. When several pages cover the same news, keep the most original source.

### 4. Filter

Drop any candidate that:

- appears in `seen.md` (compare URLs after removing tracking parameters like `utm_*` and trailing slashes),
- matches anything in the Not interested section,
- falls outside the lookback window,
- duplicates another candidate's story,
- is reference material rather than literature: documentation, changelogs, release-note pages, help-center articles, spec pages or API references. A useful test is that literature has an author and a single publication date, while reference pages are updated in place.

### 5. Fetch and verify

Fetch every shortlisted candidate (around 15) before writing about it. Every "Why it's here" line must come from the page you actually fetched in this run, never from memory, the title, or a search snippet. This is the main protection against confident descriptions of articles that don't say what you think, or links that don't exist.

If a page can't be fetched (paywall, error, login wall), drop it and list it under Run notes as skipped.

### 6. Rank and fill the slots

The research note has three slot types:

- **7 interest slots** for core and learned interests.
- **2 adjacent slots** for Exploring topics one step from what the user likes.
- **1 wildcard slot** for a bigger leap that still connects loosely to their interests.

Rank interest-slot candidates by, in order: how specifically they match an interest, technical depth or novelty, source quality, and recency. Popularity is not relevance. A trending post that only matches a broad theme should lose to a niche post that hits a specific interest.

Keep the list varied: no more than 2 items on the same subtopic and no more than 3 from the same site.

For exploring slots, pick from topics already in the Exploring section first. If there aren't enough (common on early runs), propose a new topic derived from the user's likes. Mark it as a new suggestion and include a "because" line naming the interest it grew from, so `/learn` can add it to the Exploring section. Don't suggest topics in Retired explorations unless they were retired more than 60 days ago. Choose exploring topics because they connect to the user's interests, not because they are trending.

If a slot has no strong candidate, leave it empty and say so in Run notes rather than padding.

### 7. Write the research note

Write it to `inbox/YYYY-MM-DD Research.md` using the template below. Keep each "Why it's here" to one or two sentences in your own words; don't paste article text. Give every item both checkboxes, exactly as shown, because `/learn` reads them.

### 8. Update seen.md

Append every URL included in the research note, one per line, in this format:

```
- YYYY-MM-DD https://example.com/article
```

Only add URLs that made it into the research note. Candidates that were filtered out may still be worth showing on a later day.

### 9. Finish

End with a short plain summary of the run (items written, slots left empty, pages skipped). When running on a schedule, this ends up in the run log.

## Research note template

```markdown
---
date: YYYY-MM-DD
type: research
status: pending
---
# AI engineering research: YYYY-MM-DD

Tick Like to keep an article, or Not for me to teach the profile. Then run /learn.

## Your interests

### 1. [Article title](https://example.com/article)
- **Source:** Site name · published YYYY-MM-DD
- **Matches:** speculative decoding (learned)
- **Why it's here:** One or two sentences, based on the fetched page.
- [ ] Like
- [ ] Not for me

## Exploring

### 8. [Article title](https://example.com/article)
- **Source:** Site name · published YYYY-MM-DD
- **Exploring:** KV cache compression (adjacent)
- **Because:** you liked several speculative decoding articles
- **Why it's here:** One or two sentences, based on the fetched page.
- [ ] Like
- [ ] Not for me

### 10. [Article title](https://example.com/article)
- **Source:** Site name · published YYYY-MM-DD
- **Exploring:** Developer behavior with AI coding tools (wildcard, new suggestion)
- **Because:** you like evals work; this is the human side of measuring tools
- **Why it's here:** One or two sentences, based on the fetched page.
- [ ] Like
- [ ] Not for me

## Run notes
- Lookback: since YYYY-MM-DD
- Trusted sources checked: N
- Skipped (couldn't fetch): ...
- Empty slots: ...
- Other notes: ...
```

Number items continuously across both sections. The `status: pending` field tells `/learn` the research note hasn't been processed yet.

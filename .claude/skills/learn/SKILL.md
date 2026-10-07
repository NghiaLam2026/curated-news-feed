---
name: learn
description: Process ticked items in pending AI engineering research notes. Summarize liked articles into a dated note in daily/, update interests.md from likes and dislikes, and propose bigger profile changes for approval. Use whenever the user runs /learn, says they've ticked or picked articles, or asks to process, save, or file today's research note.
---

# Learn from your picks

The user has read a research note in `inbox/` and ticked Like or Not for me on some items. This skill turns those ticks into two lasting things: a daily note of summaries they can search months later, and an updated interest profile that shapes tomorrow's research note.

Unlike `/research`, this runs while the user is present. Make small, routine changes automatically. For anything that changes what the user will see long term, propose it and wait for approval.

## Files in the vault

| File | Access | Purpose |
|---|---|---|
| `inbox/*.md` | read + update | Research notes to process (`status: pending`) |
| `daily/` | write | One note per research date with summaries of liked articles |
| `interests.md` | read + update | The profile. This skill is its only writer |
| `inbox/archive/` | write | Where processed research notes go |

Never edit the Core interests section of `interests.md`. The user writes it by hand, and it anchors the profile so learned changes can't drift away from what they stated on purpose.

## Steps

### 1. Find pending research notes

Look in `inbox/` for research notes with `status: pending`. If there are none, tell the user and stop. If there are several (the user skipped some days), process them all, oldest first. Each research note produces its own daily note dated by the research note's date, so each day keeps its own entry.

### 2. Read the ticks

For each item:

- **Like ticked:** save it (step 3) and count it as a like.
- **Not for me ticked:** count it as a dislike. Don't save it.
- **Both ticked:** treat it as a like, and mention the conflict in your final message.
- **Neither ticked:** ignore it. An unticked item usually means the user was busy, not uninterested, so it shouldn't move the profile in either direction.

Note each item's slot type (interest, adjacent, or wildcard) and topic from the research note labels. Step 4 uses them.

### 3. Write the daily note

Fetch every liked article again and summarize from the fetched page, never from the research note blurb or memory. If a page can't be fetched, still add the entry with its link and source, and write "Summary pending: couldn't fetch" instead of a summary, so the user can retry later.

Write summaries for someone searching this vault months from now, possibly a teammate who never saw the article. That reader needs to know what the article is about and whether to reopen it. So:

- Name the specific techniques, models, tools, and datasets involved. These names are what later searches will match on.
- Include concrete results and tradeoffs when the article has them (speedups, accuracy changes, costs, limitations).
- Say when the approach applies and when it doesn't, if the article makes that clear.
- Use your own words. Keep the summary to a few sentences plus a few key points, and don't paste article text.

**Tags:** give each article 2 to 4 lowercase, hyphenated tags. Before inventing a tag, check tags already used in `daily/` and reuse them, so the vault doesn't fill up with synonyms like `rag` and `retrieval-augmented-generation`. Searchability depends on a consistent vocabulary.

If `daily/YYYY-MM-DD.md` already exists (for example from an earlier run), add new entries to it and skip any URL that's already there.

Use this template:

```markdown
---
date: YYYY-MM-DD
type: daily
tags: [speculative-decoding, inference, evals]
---
# YYYY-MM-DD

## [Article title](https://example.com/article)
- **Source:** Site name · published YYYY-MM-DD
- **Tags:** #speculative-decoding #inference
- **Found via:** interests (learned: speculative decoding)

**Summary:** A few sentences on what the article covers, the method, and the result.

**Key points:**
- Concrete technique, number, or tradeoff
- Concrete technique, number, or tradeoff

**My take:** Only include this line if the user gives one in step 6.
```

The frontmatter `tags` is the combined list for the whole day. For exploring items, write "Found via: exploring (adjacent: KV cache compression)" or "(wildcard: ...)".

### 4. Update interests.md

Make these changes automatically, and add one changelog line for each, with the date and the reason.

**Learned interests**
- Liked item matching a learned interest: add the research note date to its evidence (keep only the 5 most recent dates).
- Liked item on a specific subtopic not yet listed (even under a core interest): add it as a learned interest with strength emerging. One like is a hint, not a pattern, which is why it starts low.
- Recalculate each learned interest's strength from likes in the last 30 days: 1 is emerging, 2 to 3 is medium, 4 or more is high.
- Decay: if a learned interest has no likes in the last 30 days, drop it one level. Temporary project interests fade this way instead of crowding the feed forever.

**Exploring**
- For every exploring item that appeared in the research note, add 1 to its shown count. If it was liked, add 1 to its liked count.
- If the research note marked a topic as a new suggestion, add it to the Exploring section with its "because" line and its counts. Adding a topic to Exploring is low stakes, since exploring is meant for trying things out.
- Keep at most 5 topics in Exploring. If an addition pushes it past 5, propose retiring the weakest one in step 5.

### 5. Propose bigger changes

These changes shape the profile long term, so propose them instead of applying them:

- **Graduate:** an exploring topic with 2 or more likes moves to Learned interests at strength medium.
- **Retire exploring:** an exploring topic shown 5 or more times with no likes, or marked Not for me twice, moves to Retired explorations with the date.
- **Remove learned:** a learned interest that has decayed below emerging is removed.
- **Not interested:** a subtopic marked Not for me twice within 30 days is added to the Not interested section.

Before proposing anything, check the changelog. If the user declined the same proposal in the last 30 days, don't raise it again yet.

### 6. Ask once

Send the user a single message that includes:

1. What was saved: the number of articles and the daily note path.
2. The automatic profile changes, in one line each.
3. Proposals, numbered, each with its reason in a short phrase (for example "Graduate KV cache compression: 2 likes this week").
4. An optional request for a one-line take on any saved article, which goes in that entry's "My take" line. Make it clearly optional.

Apply the proposals the user approves. Log declined proposals in the changelog as "declined" so they aren't raised again for a while. If the user skips the takes, leave the My take lines out entirely rather than writing empty ones.

If there are no proposals, skip that part of the message.

### 7. Archive

Set each processed research note's frontmatter to `status: done` and move it to `inbox/archive/`. Keeping it, rather than deleting it, preserves the record of what was shown, which helps when tuning the ranking later.

## Changelog format

Add lines to the Changelog section of `interests.md`:

```
- YYYY-MM-DD: added evidence to speculative decoding (liked "Article title")
- YYYY-MM-DD: KV cache compression shown 3, liked 2
- YYYY-MM-DD: graduated KV cache compression to learned (approved)
- YYYY-MM-DD: proposed retiring federated learning (declined)
```

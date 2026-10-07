# AI engineering reading vault

This folder is an Obsidian vault and a Claude Code project. It holds a daily reading system for AI engineering: `/research` finds and ranks articles each morning, the user ticks what they like in Obsidian, and `/learn` saves summaries and updates the interest profile. Over time the vault becomes a searchable record of everything the user found worth reading, used by them and their team.

## Layout

| Path | What it is | Who writes it |
|---|---|---|
| `interests.md` | Interest profile | User (Core section), `/learn` (everything else) |
| `sources.md` | Trusted sites to check first | User |
| `seen.md` | Every URL shown in a research note | `/research` (append only) |
| `inbox/` | Daily research notes waiting for ticks | `/research` creates, `/learn` processes |
| `inbox/archive/` | Processed research notes | `/learn` |
| `daily/` | One note per day with summaries of liked articles | `/learn` |

## Rules for every session

These apply to both skills and to any other work in this vault.

- **Write only from what you fetched.** Any description or summary of an article must come from a page fetched in the current session, never from memory, a title, or a search snippet. Unverified summaries would quietly corrupt a vault meant to be trusted later.
- **Read papers in full.** For arXiv papers, fetch the full text (the HTML version at `arxiv.org/html/<id>`, or the PDF), not just the abstract page. Say in the summary that it's a preprint unless it has been published at a venue.
- **Use your own words.** Summarize; don't paste article text. Store the link so the original is always one click away.
- **Never edit the Core interests section** of `interests.md`. The user owns it.
- **Respect file ownership** in the table above. In particular, only `/learn` changes `interests.md`, so the two skills never overwrite each other.
- **Use local dates** in `YYYY-MM-DD` format everywhere: filenames, frontmatter, and logs.
- **Newest first.** A research note has 10 items in two sections, and each section is sorted on its own by published date, latest first:
  - **Your interests** (7 items): newest at the top, oldest at the bottom.
  - **Exploring** (3 items, the adjacent and wildcard slots together): newest at the top, oldest at the bottom.

  Number items in the order they appear, continuing from the first section into the second. Break date ties by relevance. Ranking still decides which items make the cut, but not the order they are shown in.
- **Reuse existing tags.** Tags are lowercase and hyphenated (`speculative-decoding`). Check tags already used in `daily/` before creating a new one, so the vault doesn't fill up with synonyms.
- **Don't run git commands** unless the user asks. They manage sync and commits themselves.

## Answering questions about past reading

When the user or a teammate asks something like "what have we read about KV cache compression?" or "find that article on eval contamination":

1. Search `daily/` by tags and keywords, including related terms (for example both `rag` and `retrieval`).
2. Answer from the notes you find, citing each one by date and linking the original article.
3. If nothing in the vault matches, say so plainly. You can then offer general knowledge or a web search, but keep it clearly separate from what's in the notes. People asking this way want to know what's actually in the vault.
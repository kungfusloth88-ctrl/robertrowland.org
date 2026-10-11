# robertrowland.org

A simple static GitHub Pages site for a personal archive and field-note system.

## Site structure

- `index.html`: homepage and entry interaction.
- `archive/index.html`: archive layout, search, and date grouping.
- `data/notes.js`: source of truth for archive entries.
- `notes/YYYY/MM/DD/slug/index.html`: individual note pages.
- `CNAME`: custom domain configuration.

## How to add a new note

1. Choose a date and a unique, lowercase, hyphen-separated slug.
2. Create the note page at `notes/YYYY/MM/DD/slug/index.html`.
3. Copy an existing note page and update only the new page's content and metadata, preserving the existing CSS and navigation.
4. Add an entry to `window.NOTES` in `data/notes.js`.
5. Make sure the note page URL exactly matches the `url` field in `data/notes.js`.
6. Preview the site locally if possible.
7. Verify the page, archive entry, search, links, and browser console.
8. Review the diff before committing or opening a pull request. Merge only after review.

Example URL mapping:

```text
/notes/2026/10/09/example-note/
```

maps to:

```text
notes/2026/10/09/example-note/index.html
```

## Required `data/notes.js` fields

Each note entry should include these fields:

| Field | Purpose |
|---|---|
| `id` | Unique lowercase identifier, usually the slug. |
| `title` | Display title in the archive. |
| `date` | Date in `YYYY-MM-DD` format. |
| `type` | Content type, such as `field note`, `after-action note`, `conversation flow`, `essay`, `screenplay`, `media`, or `source note`. |
| `status` | Draft/public status, such as `public draft`, `rough public note`, or `private draft`. |
| `summary` | Short description used for search/context. |
| `sourceTitle` | Source or origin label. |
| `sourceUrl` | Source URL, or `null` when unavailable/not public. |
| `sourceAccessed` | Access or analysis date in `YYYY-MM-DD` format. |
| `llmUsed` | `true` or `false`. |
| `llmTool` | LLM/tool name, or `null` if none. |
| `llmDate` | LLM-assisted work date in `YYYY-MM-DD` format, or `null`. |
| `tags` | Array of searchable topic tags. |
| `url` | Public note URL. Must match the page path. |

## Copyable `data/notes.js` entry example

```js
{
  id: "example-note",
  title: "example note",
  date: "2026-10-09",
  type: "field note",

  status: "public draft",

  summary: "A short summary of what this note is about.",

  sourceTitle: "Source or origin label",
  sourceUrl: null,
  sourceAccessed: "2026-10-09",

  llmUsed: true,
  llmTool: "ChatGPT",
  llmDate: "2026-10-09",

  tags: [
    "example",
    "field note",
    "archive"
  ],

  url: "/notes/2026/10/09/example-note/"
}
```

## Local preview

This site does not use a framework, package manager, or build step.

To preview locally from the repository root:

```bash
python3 -m http.server 8000 --bind 127.0.0.1
```

Then open:

```text
http://127.0.0.1:8000/
```

## Review checklist

Before committing or merging a note change:

- The note page exists at `notes/YYYY/MM/DD/slug/index.html`.
- The `url` in `data/notes.js` matches the note page path.
- The archive displays the note under the correct date.
- Archive search finds the note by title and relevant tags.
- Clicking the archive entry opens the note page without a 404.
- Existing homepage behavior is unchanged.
- Existing archive layout/search behavior is unchanged.
- No new framework, dependency, build step, or package manager was added.

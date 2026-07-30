---
title: "A Readable, Editable Markdown View in VS Code (No More Raw .md Text)"
created: 2026-07-30
tags:
  - vscode
  - markdown
  - drawio
  - productivity
---

> *One setting change turns every `.md` file in VS Code into a formatted, click-to-edit document instead of raw markdown source.*

By default, VS Code opens `.md` files as plain text — headings show up as `## Heading`, bold text as `**bold**`, and you either read the syntax noise or pop open a separate preview pane that you can't type into. Neither is great for actually working in a notes vault day to day.

## The fix: repurpose the Draw.io extension's markdown editor

The [Draw.io Integration](https://marketplace.visualstudio.com/items?itemName=hediet.vscode-drawio) extension (`hediet.vscode-drawio`) — normally installed for embedding diagrams in markdown — also ships its own custom editor for markdown files: `drawio-inline-editor.markdownEditor`. It renders the document formatted (headings, bold, lists, etc. all styled) *and* lets you edit directly in that rendered view, rather than editing raw syntax and switching to a preview to check it.

The trick is telling VS Code to use that editor as the **default** for every `.md` file, via `workbench.editorAssociations` in `settings.json`:

```json
"workbench.editorAssociations": {
    "*.md": "drawio-inline-editor.markdownEditor"
}
```

With that in place, opening any markdown file — a note, a README, a plan doc — lands you straight in the human-readable, editable view. No extra click into preview mode, no toggling back and forth.

## Setup

1. Install the [Draw.io Integration extension](https://marketplace.visualstudio.com/items?itemName=hediet.vscode-drawio) from the marketplace.
2. Add the `workbench.editorAssociations` entry above to your user or workspace `settings.json`.
3. Reopen any `.md` file — it now opens in the formatted, editable view by default.

If you ever need the raw source (e.g. to eyeball exact markdown syntax or resolve a merge conflict), right-click the file → **Open With...** → **Text Editor**.

## The takeaway

A single `workbench.editorAssociations` entry turns an extension installed for diagrams into a lightweight WYSIWYG markdown editor for your whole vault — no separate note-taking app, no Typora, no context-switching between source and preview.

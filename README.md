# Templater for Bases

*[Русский](./README.ru.md)*

Pin a [Templater](https://github.com/SilentVoid13/Templater) template to a specific view of an
Obsidian [Base](https://help.obsidian.md/bases), and create new notes from it with two small
buttons in the Base's own toolbar — without touching your existing notes.

## What it does

- Adds a gear and a "+" button to the toolbar of any open Base.
- **Gear**: pin a Templater template to the view you're currently looking at.
- **+**: create a new note from that view's pinned template.
  - If this specific view has no template of its own yet, it borrows the template from any
    other view of the same Base and pins it here too (from then on the two are independent —
    changing one doesn't change the other).
  - The very first template you pin in a Base is copied to every view that Base already has —
    so if you only ever want one template for the whole Base, one click is all it takes.
- After creating a note, the plugin reads the active view's filters (`.base` file) and — on a
  best-effort basis — fills in whatever the template didn't already set: matching properties,
  tags/aliases, required name prefix, and target folder — so the new note actually shows up in
  the filtered table instead of vanishing from view.
- Works with a Base embedded in a note (`![[Something.base]]`), not just a Base opened as its
  own tab.

## Requirements

- Templater must be installed and enabled — this plugin creates notes through Templater's own
  note-creation routine, it doesn't reimplement template processing.
- Obsidian with Bases (a core feature since Obsidian 1.9+).
- Desktop only for now (mobile's Bases toolbar layout hasn't been verified against this plugin).

## Installation

No official Community Plugins listing yet. Install manually:

1. Download `main.js`, `manifest.json`, and `styles.css` from a release.
2. Create `<your vault>/.obsidian/plugins/templater-for-bases/` and put the three files there.
3. Reload Obsidian, then enable **Templater for Bases** in Settings → Community plugins.

## Settings

- **Interface language** — Russian, English, or Chinese. Only affects this plugin's own
  notices and settings text.
- **Where to open new notes** — new tab, split, or the current tab (replacing the Base, like
  Obsidian's native "+ New" button does).
- **Clean up orphaned pins** — removes pins pointing at `.base` files that no longer exist
  (e.g. deleted outside Obsidian). Only touches this plugin's own stored settings — never a
  note, never a `.base` file.

## Data safety

Every write this plugin makes falls into exactly one of these:

- Its own plugin data (which template is pinned where) — never your vault content.
- A **new** file created through Templater's own official creation routine.
- Filling in *unset* frontmatter fields, or adding list items (tags/aliases) on top of what
  the template already set, on that same brand-new note — never overwriting what the template
  put there on purpose.
- Renaming or moving that same brand-new note, if a filter needs it — never a pre-existing one.

It never modifies, renames, or deletes an existing note, and never writes to the `.base` file
itself (only reads it, to know the current filters and view names).

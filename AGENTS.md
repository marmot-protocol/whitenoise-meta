This vault tracks UX/UI design and product work for **White Noise**, a privacy-focused encrypted messaging mobile app.

## Vault Purpose

- Product decisions, specs, and roadmaps
- UX research and design documentation
- UI design notes, component documentation, and design system references
- Feature planning and discovery work

## Collaboration

This vault is shared via Git across multiple contributors. Keep this in mind:

- Write notes as if others will read them — avoid unexplained jargon or personal shorthand
- Use descriptive filenames in `kebab-case`
- Avoid large binary files; link to Figma or external design tools instead of embedding images where possible
- Resolve merge conflicts carefully — Obsidian's `.md` files are plain text and generally merge cleanly, but avoid renaming files while others may be editing them

## Conventions

- **Dates**: ISO 8601 (`YYYY-MM-DD`) in filenames and frontmatter
- **Frontmatter**: Include `status`, `owner`, and `date` fields on all documents
- **Folders**: Organize by area (e.g. `Design/`, `Product/`, `Research/`)
- **Links**: Use Obsidian wiki-links (`[[note-name]]`) freely — they survive Git sync

## Related Repositories

- [whitenoise](https://github.com/marmot-protocol/whitenoise) — Flutter mobile app
- [whitenoise-rs](https://github.com/marmot-protocol/whitenoise-rs) — Rust core library
- [mdk](https://github.com/marmot-protocol/mdk) — Marmot development kit
- [marmot](https://github.com/marmot-protocol/marmot) — Marmot Protocol

## What AI Agents Should Know

If an AI agent is reading this vault:

- This is a **product and design** vault — not a code repository
- The app is called **White Noise** — a mobile encrypted messaging app built on the Marmot Protocol (MLS over Nostr)
- Do not generate or modify files unless explicitly asked
- Prefer summarizing and linking over duplicating content
- Treat all notes as potentially draft — check `status` frontmatter before assuming anything is finalized
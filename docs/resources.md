# 📎 Resources

## Scaffolding New Days

This project ships with a generator so you never hand-write folder structure
or nav entries for 160 days.

```bash
python scripts/generate_course.py
```

What it does:

1. Reads `scripts/topics.yaml` — a simple `day, title, module` list
2. Creates `docs/devops-course/day-XXX/index.md` from the template
   (skips any file that already exists, so it's safe to re-run)
3. Creates a `.pages` file per day setting its sidebar title to
   `Day XXX – Topic Name`
4. Regenerates `docs/devops-course/.pages` so the sidebar is grouped by
   module, in the exact order defined in `topics.yaml`

To add **Day 161+**: add one row to `scripts/topics.yaml`, re-run the script.
Nothing else changes — not `mkdocs.yml`, not any other file.

```yaml title="scripts/topics.yaml (excerpt)"
- day: 161
  module: "Module 13: Advanced Kubernetes"
  title: "Custom Resource Definitions (CRDs)"
```

## Local Development

```bash
# 1. Create & activate a virtual environment
python -m venv .venv
source .venv/bin/activate      # Windows: .venv\Scripts\activate

# 2. Install dependencies
pip install -r requirements.txt

# 3. Serve locally with live-reload
mkdocs serve
# → open http://127.0.0.1:8000

# 4. Build the static site
mkdocs build

# 5. Deploy to GitHub Pages
mkdocs gh-deploy --force
```

## Writing a New Day's Notes

Each `day-XXX/index.md` starts from the same template (see
[Day 001](devops-course/day-001/index.md) for a fully worked example):

```markdown
---
title: Day 01 – Linux Basics
description: One-line summary for search results / social previews.
tags:
  - linux
  - fundamentals
---

# Day 01 – Linux Basics

## 🎯 Overview
## 📺 Video Info
## 🧠 Learning Objectives
## 📝 Core Notes
## 💻 Commands Reference
## 🖼️ Diagrams
## ⚠️ Common Errors & Gotchas
## ❓ Interview Questions
## ✅ Summary
## 🔗 Related Days
```

!!! tip "Front matter `tags`"
    Add a `tags:` list to any page's front matter and it will automatically
    show up in a searchable tag index once you enable the `tags` plugin (see
    [Material's tags docs](https://squidfunk.github.io/mkdocs-material/setup/setting-up-tags/)).

## Markdown Cheat Sheet (features enabled on this site)

| Feature | Syntax |
|---|---|
| Admonition | `!!! note "Title"` |
| Collapsible block | `??? note "Title"` (add `+` to open by default: `???+`) |
| Tabs | `=== "Tab name"` |
| Code annotation | `# (1)!` next to a line, then `1. Explanation` below the block |
| Keyboard keys | `++ctrl+c++` → ++ctrl+c++ |
| Task list | `- [x] Done` / `- [ ] Todo` |
| Footnote | `Text[^1]` ... `[^1]: Note` |
| Mermaid diagram | ` ```mermaid ` fenced code block |
| Math | `\( inline \)` or `\[ display \]` |

## External References

- [MkDocs Material — official docs](https://squidfunk.github.io/mkdocs-material/)
- [Mermaid.js syntax reference](https://mermaid.js.org/intro/)
- [PyMdown Extensions reference](https://facelessuser.github.io/pymdown-extensions/)
- [Kubernetes documentation](https://kubernetes.io/docs/home/) — structural inspiration
- [Terraform documentation](https://developer.hashicorp.com/terraform/docs) — structural inspiration

# DevOps Knowledge Base

A professional documentation site — built with **MkDocs + Material for
MkDocs** — turning a 160-video DevOps Engineering playlist into structured,
searchable, interview-ready notes.

Live structure mirrors documentation sites like Kubernetes, Docker, and
Terraform: navigation tabs, sectioned sidebar, instant search, dark/light
mode, Mermaid diagrams, and more.

## Quick Start

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

pip install -r requirements.txt

mkdocs serve                     # http://127.0.0.1:8000, live-reload
```

Build the static site:

```bash
mkdocs build      # outputs to ./site/
```

Deploy to GitHub Pages:

```bash
mkdocs gh-deploy --force
```

## Project Structure

```text
project/
│
├── docs/
│   ├── index.md                 # Home page (hero, stats, roadmap links)
│   ├── about.md
│   ├── roadmap.md
│   ├── resources.md
│   ├── stylesheets/extra.css    # Custom theme polish
│   ├── javascripts/mathjax.js   # Math support config
│   ├── diagrams/                # Optional diagram source files
│   ├── images/                  # Screenshots, logos
│   ├── assets/                  # Downloadable files (PDFs, configs)
│   └── devops-course/
│       ├── .pages               # Auto-generated module-grouped nav
│       ├── index.md             # Auto-generated module overview
│       ├── day-001/
│       │   ├── index.md
│       │   └── .pages           # Sets sidebar title "Day 001 – ..."
│       ├── day-002/
│       ├── ...
│       └── day-160/
│
├── scripts/
│   ├── topics.yaml              # Master list: day → title → module
│   ├── generate_course.py       # Scaffolds folders + rebuilds nav from topics.yaml
│   └── build_topics.py          # One-off script used to author topics.yaml
│
├── mkdocs.yml
├── requirements.txt
└── README.md
```

## Adding a New Day

1. Add a row to `scripts/topics.yaml`:
   ```yaml
   - day: 161
     module: "Module 13: Advanced Kubernetes"
     title: "Custom Resource Definitions (CRDs)"
   ```
2. Run:
   ```bash
   python scripts/generate_course.py
   ```
3. Open `docs/devops-course/day-161/index.md`, replace the stub with your notes.

`mkdocs.yml` never needs to change — the sidebar is driven entirely by the
folder structure via [mkdocs-awesome-pages-plugin](https://github.com/lukasgeiter/mkdocs-awesome-pages-plugin).

## Why 3-digit day folders (`day-001` … `day-160`)?

Two-digit folders (`day-1`, `day-10`) sort incorrectly once you pass 9 days
(`day-10` alphabetically precedes `day-2`). Zero-padding to 3 digits
(`day-001` … `day-160`) keeps folder names, URLs, and any tooling that
lists/sorts directories consistent all the way past day 999 — while the
**displayed titles** still read naturally as "Day 001 – Introduction to
Linux & DevOps" via each folder's `.pages` file.

## Tech Stack

- [MkDocs](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- [mkdocs-awesome-pages-plugin](https://github.com/lukasgeiter/mkdocs-awesome-pages-plugin) — folder-driven nav
- [mkdocs-glightbox](https://github.com/blueswen/mkdocs-glightbox) — image zoom
- [mkdocs-git-revision-date-localized-plugin](https://github.com/timvink/mkdocs-git-revision-date-localized-plugin) — "last updated" dates
- Mermaid.js — diagrams (built into Material)
- MathJax — math rendering

## Auto-Deploy on Every Push (GitHub Actions)

A workflow at `.github/workflows/deploy.yml` builds and deploys the site to
the `gh-pages` branch automatically on every push to `main` — no manual
`mkdocs gh-deploy` needed after initial setup.

Requirements:

1. In your repo: **Settings → Actions → General → Workflow permissions** →
   set to **"Read and write permissions"** (needed so the workflow can push
   to `gh-pages`).
2. In your repo: **Settings → Pages → Source** → **Deploy from a branch** →
   branch `gh-pages`, folder `/ (root)`.
3. Push to `main` — check the **Actions** tab to watch the build/deploy run.

If your default branch isn't `main`, edit the `branches:` value in
`.github/workflows/deploy.yml` to match.

## License

Personal knowledge base — reuse the structure freely for your own learning notes.


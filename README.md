# Axioms to Algorithms

Mathematics and machine learning notes from first principles.

Built with [Zola](https://www.getzola.org/).

## Local development

```bash
zola serve
```

Open http://127.0.0.1:1111

## Build

```bash
zola build --base-url "https://ahmad-sardar.github.io"
```

Output is written to `docs/` for GitHub Pages.

## Content

- `content/` — Markdown pages
- `static/` — CSS, images, and interactive visualizations
- `templates/` — HTML layouts and shortcodes

To regenerate markdown from legacy Quarto sources (if retained), run:

```bash
python3 scripts/convert_qmd.py
```

## Deploy

Pushes to `main` trigger `.github/workflows/publish.yml`, which builds with Zola and deploys to GitHub Pages.

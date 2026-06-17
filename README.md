# Italiensk – Sætningsbyggeren 🇮🇹

[![Pages](https://img.shields.io/badge/live-GitHub%20Pages-2e7d4f?logo=github)](https://strudso.github.io/italian-tables/)
[![Stars](https://img.shields.io/github/stars/STRUDSO/italian-tables?style=flat&logo=github&color=2e7d4f)](https://github.com/STRUDSO/italian-tables/stargazers)
[![Forks](https://img.shields.io/github/forks/STRUDSO/italian-tables?style=flat&logo=github)](https://github.com/STRUDSO/italian-tables/network/members)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Made with Claude Code](https://img.shields.io/badge/made%20with-Claude%20Code%20(Opus%204.8)-d97757)](https://claude.com/claude-code)

A tiny, dependency-free web app for learning to build simple **Italian** sentences,
grown from **two handwritten study notes**:

- **Tabel 1 – Udsagnsord:** present-tense conjugation (`io`→`loro` × `-are`/`-ere`/`-ire`)
- **Tabel 2 – Navneord & artikler:** gender × indefinite/definite/plural article patterns

Pick a **person**, a **form** (ubestemt / bestemt / flertal), a **noun**, a **verb**, and an
**adjective** — the app conjugates the verb, chooses the right article, agrees the adjective,
and **shows you exactly which table cell each part came from**.

## 🔗 Live

| View | URL | What it does |
|------|-----|--------------|
| 🔍 **Fokuseret udsnit** | [`/focus/`](https://strudso.github.io/italian-tables/focus/) | A focused "zoom-in" slice of each table under the builder, full tables below. |
| 🔗 **Ord-sporing** | [`/trace/`](https://strudso.github.io/italian-tables/trace/) | Sentence as colored word-chips; hover for the source bubble, click to scroll the table. |

Landing page: **https://strudso.github.io/italian-tables/**

## 🧑‍🍳 How it was made

Built conversationally with **Claude Code (model: Opus 4.8)**: two phone photos of handwritten
notes (`.heic`) were converted and transcribed, turned into an interactive sentence builder,
then iterated through several visualization prototypes (a few drafted in parallel by a small
team of agents) before settling on the two views shipped here. The full "recipe" is on the
landing page.

## 🛠️ Run locally

No build step, no dependencies. Just open the files:

```bash
git clone https://github.com/STRUDSO/italian-tables.git
cd italian-tables
open index.html        # macOS — or just double-click it
```

Each page is a single self-contained HTML file (inline CSS + vanilla JS).

## 📁 Structure

```
.
├── index.html        # landing / gallery + the "recipe"
├── focus/index.html  # View A — focused slice
├── trace/index.html  # View B — token tracing
└── LICENSE
```

## 🤝 Contributing

Ideas, more verbs/nouns/adjectives, or new visualizations are welcome — open an issue or a PR.

## 📄 License

[MIT](LICENSE) © 2026 STRUDSO

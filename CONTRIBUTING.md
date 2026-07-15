# Contributing to TPS

Thank you for your interest in contributing to the **Trading Product Specification (TPS)** project! 🎉

We welcome contributions of all kinds — documentation, schema definitions, design tokens, examples, and more.

---

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How to Contribute](#how-to-contribute)
- [Branch Naming Convention](#branch-naming-convention)
- [Commit Message Convention](#commit-message-convention)
- [Pull Request Process](#pull-request-process)
- [Issue Reporting](#issue-reporting)

---

## Code of Conduct

Please read our [Code of Conduct](./CODE_OF_CONDUCT.md) before contributing.

---

## How to Contribute

1. **Fork** this repository

2. **Clone** your fork locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/TPS.git
   cd TPS
   

3. **Create a branch** following our naming convention

4. **Make your changes**

5. **Commit** with a clear message

6. **Push** and open a **Pull Request**

## Branch Naming Convention

| Type    | Format                    | Example                   |
| :------ | :------------------------ | :------------------------ |
| Feature | `feat/short-description`  | `feat/add-order-schema`   |
| Fix     | `fix/short-description`   | `fix/button-spec-typo`    |
| Docs    | `docs/short-description`  | `docs/update-terminology` |
| Chore   | `chore/short-description` | `chore/update-ci`         |

------

## Commit Message Convention

We follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

```
arduino

<type>: <short summary>  

[optional body]  
```

**Types:**

- `feat` — New specification content
- `fix` — Fix errors or inconsistencies
- `docs` — Documentation updates
- `chore` — Maintenance tasks
- `refactor` — Restructuring without content change

**Examples:**

```
vbnet

feat: add ORDER domain specification  
fix: correct margin calculation formula in MARGIN.md  
docs: update TERMINOLOGY with options glossary  
```

------

## Pull Request Process

1. Ensure your branch is up to date with `main`
2. Fill in the Pull Request template completely
3. Link related Issues in the PR description
4. Wait for review — all PRs require at least **1 approval**
5. Squash and merge upon approval

------

## Issue Reporting

- Use the provided Issue templates
- Search existing issues before creating a new one
- Be specific and provide context

------

Thank you for helping build the future of trading platform specifications! 🚀

```
yaml





---  

## 📄 `ROADMAP.md`  

```markdown  
# TPS Roadmap  

> **Trading Product Specification** — An AI-native open specification for professional trading platforms.  

---  

## 🏁 Milestone 1 — Repository Scaffold ✅  

**Goal:** Establish a production-grade open source repository structure.  

- [x] GitHub repository created (Public, Apache 2.0)  
- [x] `README.md` — Project introduction  
- [x] `MANIFEST.md` — Project manifest  
- [x] `LICENSE` — Apache 2.0  
- [x] `CHANGELOG.md` — Version history  
- [x] `CONTRIBUTING.md` — Contribution guide  
- [x] `CODE_OF_CONDUCT.md` — Code of conduct  
- [x] `SECURITY.md` — Security policy  
- [x] `ROADMAP.md` — This file  
- [x] `package.json` — Project scripts  
- [x] `docusaurus.config.js` — Docs site config  
- [x] `.editorconfig` — Editor config  
- [x] Directory skeleton initialized  
- [x] `.github/` — Issue templates, PR template, GitHub Actions CI  

---  

## 🔄 Milestone 2 — Foundation Docs  

**Goal:** Complete all foundational specification documents.  

- [ ] `docs/foundations/PRINCIPLES.md` — Core design principles  
- [ ] `docs/foundations/DESIGN.md` — Design philosophy  
- [ ] `docs/foundations/PRODUCT.md` — Product definition  
- [ ] `docs/foundations/MARKET.md` — Market context  
- [ ] `docs/foundations/TERMINOLOGY.md` — Unified glossary  
- [ ] `docs/foundations/AI_RULES.md` — AI usage rules  
- [ ] `docs/foundations/ANTI_PATTERNS.md` — Anti-patterns  
- [ ] `docs/foundations-ui/COLOR.md`  
- [ ] `docs/foundations-ui/TYPOGRAPHY.md`  
- [ ] `docs/foundations-ui/SPACING.md`  
- [ ] `docs/foundations-ui/GRID.md`  
- [ ] `docs/foundations-ui/LAYOUT.md`  
- [ ] `docs/foundations-ui/MOTION.md`  
- [ ] `docs/foundations-ui/ICONOGRAPHY.md`  
- [ ] `docs/foundations-ui/ACCESSIBILITY.md`  

---  

## 📋 Milestone 3 — Schemas, Tokens & Components  

**Goal:** Deliver machine-readable schemas, design tokens, and first component specs.  

- [ ] `schemas/` — JSON Schema for Quote, Order, Account, Button, Timeline  
- [ ] `tokens/` — Design Tokens (color, typography, spacing, motion)  
- [ ] `examples/` — Reference examples (Watchlist, Order Entry, Dashboard)  
- [ ] `prompts/` — Official AI prompts (Cursor, Claude, Gemini, ChatGPT)  
- [ ] `docs/components/` — First batch: QUOTE, TIMELINE, ORDER_ENTRY  
- [ ] `docs/domains/` — First batch: ORDER, ACCOUNT, EXECUTION  
- [ ] `docs/markets/` — US, HK, CN  

---  

## 🔮 Future Plans  

| Direction | Description |  
|-----------|-------------|  
| 📖 Docs Site | GitHub Pages + Docusaurus |  
| 🧩 VS Code Extension | TPS spec integration in editor |  
| 🛠️ TPS CLI | Command-line tool for spec generation |  
| 🎨 Figma Plugin | Design tool integration |  
| 🌍 i18n | Multi-language specification support |  
```
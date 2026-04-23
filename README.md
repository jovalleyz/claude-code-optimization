# Claude Code Optimization

**65-75% token reduction for Claude Code sessions** | Production-ready templates for any project

---

## 🎯 What This Is

Templates and guides to optimize Claude Code context loading:

- **`claude.md`** — Auto-loaded context for every session
- **`MEMORY-CORE.md`** — Compressed essentials (schema, endpoints, patterns)
- **`.claudeignore`** — Files Claude should NOT load

**Result:** Save 30-40% tokens session 1, **65-75% session 2+** with caching + compaction.

---

## 🚀 Quick Start

### For a New Project

1. Copy templates to your project root:
```bash
cp claude.md-TEMPLATE claude.md
cp MEMORY-CORE.md-TEMPLATE MEMORY-CORE.md
cp .claudeignore-TEMPLATE .claudeignore
```

2. Customize placeholders (10 minutes):
   - Replace `[PROJECT_NAME]`
   - Add your stack, schema, endpoints
   - Personalize patterns for your codebase

3. Commit + push:
```bash
git add claude.md MEMORY-CORE.md .claudeignore
git commit -m "docs: add claude code optimization"
git push
```

4. Open Claude Code:
   - Claude **automatically** loads your context
   - No setup needed

---

## 📖 Full Guide

See **[SETUP-GUIDE.md](./SETUP-GUIDE.md)** for:
- Step-by-step setup
- Tips by project type (Frontend, Backend, Full Stack, AI/ML)
- How to update over time
- FAQ + troubleshooting

---

## 📊 How It Works

### Before Optimization

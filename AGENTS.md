# AGENTS.md — AI Coding Agent Instructions

> Link to full documentation: [README.md](README.md)

## Project Overview

- **Framework**: Vue 3 (Composition API) + Vite
- **Language**: JavaScript (ES Modules)
- **Build Tool**: Vite 8.x

## Commands

| Command | Action |
|---------|--------|
| `npm run dev` | Start dev server (localhost) |
| `npm run build` | Production build |
| `npm run preview` | Preview production build |

## Key Files

| File | Purpose |
|------|---------|
| [src/App.vue](src/App.vue) | Main app component with routing (page state) |
| [src/main.js](src/main.js) | App entry point |
| [src/style.css](src/style.css) | Global styles |
| [vite.config.js](vite.config.js) | Vite configuration |

## Architecture

- **Routing**: Client-side via `page` reactive state (no vue-router)
- **State**: Vue 3 `ref` / `reactive` for local state
- **Components**: Single-file components in `src/components/`

## Conventions

- Use `<script setup>` syntax for Vue components
- CSS classes follow BEM-like naming (e.g., `nav-glass`, `hero-bg`)
- Dark mode via `isDark` ref and `.dark` class on root div

## Notes

- No TypeScript in this project
- No scrolling libraries currently in use
- Project uses vanilla CSS (no Tailwind/SCSS)
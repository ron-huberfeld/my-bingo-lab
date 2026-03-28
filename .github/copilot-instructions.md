# Bingo Mixer — Workspace Guidelines

Automated instruction file for GitHub Copilot across this workspace.

## Before Committing ☑️

Always run before pushing code:
- [ ] `npm run lint` — TypeScript-ESLint check
- [ ] `npm run build` — Vite production build (type check + bundle)
- [ ] `npm run test` — Vitest unit tests

## Code Style

- **TypeScript**: [React 19](src/App.tsx) + strict mode, functional hooks only, named exports
- **Naming**: PascalCase for components, camelCase for functions/variables
- **CSS**: [Tailwind CSS v4](https://tailwindcss.com/docs/v4)—use `@theme` directive, not v3 `--tw-*` syntax

## Architecture

Frontend-only SPA: [App.tsx](src/App.tsx) routes to game states. Single `useBingoGame` hook manages state + localStorage. Pure utils in [src/utils/bingoLogic.ts](src/utils/bingoLogic.ts). Types in [src/types/index.ts](src/types/index.ts). GitHub Pages deployment requires `VITE_REPO_NAME` env var.

## Dev Commands

```bash
npm install        # Node 22+ required (ES modules)
npm run dev        # Vite dev server http://localhost:5173 (hot reload)
npm run build      # TypeScript check + prod bundle → dist/
npm run test       # Vitest (jsdom)
npm run lint       # ESLint + TypeScript-ESLint
```

## File Structure

- **`src/components/`** — PascalCase `.tsx`, named exports
- **`src/hooks/`** — camelCase with `use` prefix (state + side-effects)
- **`src/utils/`** — Pure, deterministic functions ([bingoLogic.ts](src/utils/bingoLogic.ts) example)
- **`src/data/`** — Static [questions.ts](src/data/questions.ts) with FREE_SPACE constant
- **localStorage** — Includes `version` field for schema validation; always validate on retrieval

## Key Constraints

- **Strict TypeScript** — No implicit `any`, handle all types explicitly
- **GitHub Pages base path** — `VITE_REPO_NAME` env var must match repo name; breaks on localhost without it
- **Tailwind v4 (@theme)** — Use new directive, not v3 `--tw-*` syntax
- **localStorage** — Board state persists; clear manually if resetting needed

## Resources

[Lab Guide](workshop/GUIDE.md) | [Design](workshop/02-design.md) | [Tailwind](./github/instructions/tailwind-4.instructions.md) | [Frontend Skill](.github/skills/frontend-design/SKILL.md)

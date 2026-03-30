```markdown
# cloudflare_temp_email Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches you how to contribute to the `cloudflare_temp_email` codebase, a TypeScript project for temporary email services. You'll learn the repository's coding conventions, commit patterns, and the main development workflows, including dependency upgrades, feature development, bugfixing, E2E testing, documentation, CI/CD, and refactoring. This guide also covers how to write and organize tests, and provides handy slash commands for common tasks.

---

## Coding Conventions

**File Naming**
- Source files: `camelCase` (e.g., `emailHandler.ts`, `userUtils.ts`)
- Test files: `*.spec.ts` (e.g., `emailApi.spec.ts`)
- Docs: Markdown files, often in structured folders (e.g., `vitepress-docs/docs/en/guide/getting-started.md`)

**Import Style**
- Use **relative imports**:
  ```typescript
  import { getUser } from './userUtils'
  ```

**Export Style**
- Use **named exports**:
  ```typescript
  // userUtils.ts
  export function getUser(id: string) { ... }
  ```

**Commit Messages**
- Use [Conventional Commits](https://www.conventionalcommits.org/):
  - `feat:` for new features
  - `fix:` for bugfixes
  - `docs:` for documentation
  - `test:` for tests
  - `chore:` for maintenance
  - `refactor:` for code restructuring
- Example:  
  ```
  feat: add support for custom email domains
  fix: handle SMTP disconnect errors gracefully
  docs: update guide for new API endpoint
  ```

---

## Workflows

### Dependency Upgrade Across Subprojects
**Trigger:** When dependencies need to be updated for bugfixes, security, or compatibility.  
**Command:** `/upgrade-deps`

1. Update dependency versions in `package.json` or `requirements.txt`
2. Update lock files (`pnpm-lock.yaml`, `package-lock.json`)
3. Update `Dockerfile` or related CI files if needed
4. Commit with message:  
   ```
   chore(deps): upgrade dependencies
   ```
5. Example:
   ```bash
   pnpm up --latest
   git add frontend/package.json frontend/pnpm-lock.yaml
   git commit -m "chore(deps): upgrade frontend dependencies"
   ```

---

### Feature Development with Docs and Changelog
**Trigger:** When adding a new feature or significant capability.  
**Command:** `/new-feature`

1. Implement the feature in backend (`worker/src/**/*.ts`) and/or frontend (`frontend/src/**/*.vue`)
2. Update or add documentation in `vitepress-docs/docs/en/guide/` and `vitepress-docs/docs/zh/guide/`
3. Add or update `CHANGELOG.md` and `CHANGELOG_EN.md`
4. Update types or config templates if needed
5. Commit with message:
   ```
   feat: add [feature description]
   ```
6. Example:
   ```typescript
   // worker/src/emailHandler.ts
   export function enableAutoReply() { ... }
   ```
   ```
   git commit -am "feat: add auto-reply support"
   ```

---

### Bugfix with Changelog Update
**Trigger:** When a bug or regression is discovered.  
**Command:** `/bugfix`

1. Fix the bug in code (backend/frontend)
2. Update `CHANGELOG.md` and `CHANGELOG_EN.md`
3. Add or update tests if relevant
4. Commit with message:
   ```
   fix: [bug description]
   ```
5. Example:
   ```typescript
   // worker/src/emailHandler.ts
   export function parseEmail() {
     // fix: handle missing subject
   }
   ```
   ```
   git commit -am "fix: handle missing subject in email parsing"
   ```

---

### E2E Test Addition
**Trigger:** When a new feature is added or a regression/bugfix needs coverage.  
**Command:** `/add-e2e-test`

1. Create new test file in `e2e/tests/api/` or `e2e/tests/browser/`
2. Update or add helpers in `e2e/fixtures/` if needed
3. Update `e2e/fixtures/wrangler.toml.e2e` if new env vars are required
4. Commit with message:
   ```
   test: add E2E test for [feature/bug]
   ```
5. Example:
   ```typescript
   // e2e/tests/api/autoReply.spec.ts
   import { test, expect } from '@playwright/test'
   test('auto-reply works', async ({ request }) => { ... })
   ```

---

### Documentation Update
**Trigger:** When documentation needs to be improved, clarified, or synced with code changes.  
**Command:** `/update-docs`

1. Edit `vitepress-docs/docs/en/guide/**/*.md` and `vitepress-docs/docs/zh/guide/**/*.md`
2. Update `CHANGELOG.md` and `CHANGELOG_EN.md` if documenting a change
3. Edit `README.md`, `README_EN.md`, or `CLAUDE.md` if project-level docs are affected
4. Commit with message:
   ```
   docs: [description]
   ```
5. Example:
   ```
   docs: clarify API authentication section
   ```

---

### CI/CD Workflow Update
**Trigger:** When CI/CD pipeline needs to be fixed or improved.  
**Command:** `/update-ci`

1. Edit `.github/workflows/*.yml` or `.github/workflows/*.yaml`
2. Update related scripts or Dockerfiles if needed
3. Commit with message:
   ```
   fix: update CI workflow for [reason]
   ```
   or
   ```
   chore: update deployment pipeline
   ```

---

### Refactor with Test or Doc Update
**Trigger:** When code needs to be cleaned up, modularized, or reorganized.  
**Command:** `/refactor`

1. Refactor code (move, split, or rewrite files/modules)
2. Update or add tests to cover refactored logic
3. Update documentation or changelogs to reflect changes
4. Commit with message:
   ```
   refactor: [description]
   ```
5. Example:
   ```
   refactor: extract email parsing logic to utils
   ```

---

## Testing Patterns

- **Framework:** [Playwright](https://playwright.dev/)
- **Test Files:** Located in `e2e/tests/`, named `*.spec.ts`
- **Structure:**
  ```typescript
  // e2e/tests/api/emailApi.spec.ts
  import { test, expect } from '@playwright/test'

  test('should create a new temp email', async ({ request }) => {
    const response = await request.post('/api/email', { data: { ... } })
    expect(response.ok()).toBeTruthy()
  })
  ```
- **Helpers:** Place shared helpers in `e2e/fixtures/`
- **Environment:** Use `e2e/fixtures/wrangler.toml.e2e` for test-specific config

---

## Commands

| Command         | Purpose                                             |
|-----------------|-----------------------------------------------------|
| /upgrade-deps   | Upgrade dependencies across subprojects             |
| /new-feature    | Start a new feature with docs and changelog         |
| /bugfix         | Fix a bug and update changelog/tests                |
| /add-e2e-test   | Add new E2E test coverage                          |
| /update-docs    | Update or clarify documentation                     |
| /update-ci      | Update CI/CD workflows or deployment scripts        |
| /refactor       | Refactor code with supporting tests/docs            |
```

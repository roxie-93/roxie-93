# Agent Workflow & Operating Instructions

This document provides guidelines and instructions for AI agents and automated contributors working on this repository.

---

## 1. Branching Strategy

- **Never push directly to `main`**.
- Always branch off the latest `main`:
  ```bash
  git checkout main
  git pull origin main
  git checkout -b <branch-type>-<short-description>
  ```
- **Branch Naming Conventions**:
  - `feat-<feature-name>` or `feat/<feature-name>`: New additions or enhancements.
  - `fix-<fix-name>` or `fix/<fix-name>`: Bug fixes, broken links, or visual glitches.
  - `chore-<task-name>`: Maintenance, workflow changes, or repository configuration.
  - `docs-<doc-name>`: Documentation updates.

---

## 2. Commit Standards

Follow **Conventional Commits**:
- `feat: <description>` - A new feature or section
- `fix: <description>` - A bug or visual fix
- `docs: <description>` - Documentation changes (e.g. README, agent.md)
- `chore: <description>` - Workflows, config, or asset updates

Example:
```bash
git add .
git commit -m "docs: update agent instructions and add auto-merge workflow"
```

---

## 3. Creating Pull Requests

Always use the **GitHub CLI (`gh`)** to create Pull Requests with a descriptive title and body:

```bash
# Push branch to remote
git push -u origin <branch-name>

# Create Pull Request
gh pr create \
  --base main \
  --head <branch-name> \
  --title "<type>: <brief title>" \
  --body "<bulleted description of changes>"
```

---

## 4. Automated & CLI Merging

### Automated Merging (GitHub Actions)
- This repository has a GitHub Action configured in `.github/workflows/auto-merge.yml`.
- Non-draft PRs will automatically be merged into `main` and the feature branch deleted upon opening or updating.

### Manual / Fallback CLI Merge
If the automated workflow is queued or manual execution is required, merge via GitHub CLI:

```bash
# Merge PR and delete remote branch
gh pr merge <PR_NUMBER_OR_URL> --merge --delete-branch

# Sync local main
git checkout main
git pull origin main
```

---

## 5. Quality & Verification Guidelines

Before opening a PR:
1. **Verify Asset URLs**: Ensure all badge links, images, and external SVG services return valid HTTP 200 responses.
2. **Markdown Integrity**: Check that HTML tags and markdown structures are properly closed without duplicate sections.
3. **Keep it Modern & Clean**: Maintain dark-theme aesthetic consistency (`tokyonight`/GitHub dark).

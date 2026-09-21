# Courses

The private source of truth for every Xenos training course: session decks, notes, and supporting files, organized one folder per course.

**Live hub:** https://smartvision-group.github.io/courses-site/

## How this works

This repository is private, so it can't host GitHub Pages directly on a Free plan. Instead:

1. You add or edit course content **here**, in `SmartVision-Group/Courses`.
2. A GitHub Action (`.github/workflows/mirror-to-pages.yml`) mirrors the entire repository to the public repo [`SmartVision-Group/courses-site`](https://github.com/SmartVision-Group/courses-site) on every push to `main`.
3. GitHub Pages serves that public mirror at the live hub URL above.
4. `index.html` fetches the mirror's own file tree from the GitHub API at page-load time and renders it, so the hub always reflects whatever is currently in this repository. There is nothing to hand-edit when you add a course.

```
Courses (private, you edit here)
   │  git push
   ▼
GitHub Action (mirror-to-pages.yml)
   │  mirrors everything except .git and .github
   ▼
courses-site (public, GitHub Pages)
   │
   ▼
https://smartvision-group.github.io/courses-site/
```

## Adding a new course

1. Create a new top-level folder in this repository, named for the course (for example `erpnext-fundamentals`). Folder names are title-cased automatically on the hub page (`erpnext-fundamentals` becomes "Erpnext Fundamentals"), so use readable, hyphen-separated names.
2. Add its files directly inside that folder. Subfolders are supported and rendered as nested, expandable sections, so a course can grow into `x/subfolder/...` without any changes to the hub.
3. Commit and push to `main`.
4. The mirror workflow runs automatically. Give it a minute, then refresh the live hub, the new course appears in the grid on its own.

Supported file types are recognized and labeled automatically (HTML decks, PDFs, Markdown notes, videos, images); anything else still shows up as a plain file.

## One-time setup: the mirror secret

The mirror workflow needs a token with write access to `SmartVision-Group/courses-site`, stored as a repository secret named `PAGES_DEPLOY_TOKEN`. This is a one-time setup step:

1. Create a **fine-grained personal access token** at https://github.com/settings/personal-access-tokens/new
   - Resource owner: `SmartVision-Group`
   - Repository access: **Only** `courses-site`
   - Permissions: **Contents: Read and write**
2. Copy the generated token.
3. In your own terminal (not shared with anyone else), run:
   ```bash
   gh secret set PAGES_DEPLOY_TOKEN --repo SmartVision-Group/Courses
   ```
   and paste the token when prompted. (Or add it via **Settings → Secrets and variables → Actions** on the `Courses` repo.)
4. Re-run the workflow once from the **Actions** tab (or push any commit) to trigger the first mirror.

Keep the token scoped to only `courses-site` with only **Contents: Read and write** — it never needs access to this repository or anything else.

## Structure

```
Courses/
  README.md
  index.html                  → the dynamic hub page (mirrored to courses-site)
  .github/workflows/          → the mirror-to-pages automation
  software-qa-testing/        → example course: 3 session decks
    1-qa-fundamentals-intro.html
    2-developer-live-testing.html
    3-erpnext-implementer-live-testing.html
```
